# Flutter CRUD Example with SQLite

이 문서에서는 Flutter 애플리케이션에서 SQLite를 사용하여 CRUD (Create, Read, Update, Delete) 기능을 구현하는 방법을 설명합니다.

## 1. 프로젝트 설정

### 1.1. `pubspec.yaml` 파일 설정

먼저, `pubspec.yaml` 파일에 SQLite 관련 패키지를 추가합니다.

```yaml
dependencies:
  flutter:
    sdk: flutter
  sqflite: ^2.0.0+4
  path_provider: ^2.0.11
```

### 1.2. 패키지 설치

터미널에서 다음 명령어를 실행하여 패키지를 설치합니다.

```bash
flutter pub get
```

## 2. 데이터베이스 설정

### 2.1. 데이터베이스 헬퍼 클래스 생성

데이터베이스와 상호작용하기 위한 헬퍼 클래스를 생성합니다. 이 클래스에서는 데이터베이스를 열고, 테이블을 생성하며, CRUD 작업을 수행합니다.

```dart
import 'package:sqflite/sqflite.dart';
import 'package:path/path.dart';

class DatabaseHelper {
  static final DatabaseHelper _instance = DatabaseHelper._internal();
  factory DatabaseHelper() => _instance;
  static Database? _database;

  DatabaseHelper._internal();

  Future<Database> get database async {
    if (_database != null) return _database!;
    _database = await _initDatabase();
    return _database!;
  }

  Future<Database> _initDatabase() async {
    final databasePath = await getDatabasesPath();
    final path = join(databasePath, 'example.db');

    return await openDatabase(
      path,
      version: 1,
      onCreate: (db, version) {
        return db.execute(
          'CREATE TABLE items(id INTEGER PRIMARY KEY AUTOINCREMENT, name TEXT)',
        );
      },
    );
  }

  Future<int> insertItem(Map<String, dynamic> item) async {
    final db = await database;
    return await db.insert('items', item);
  }

  Future<List<Map<String, dynamic>>> getItems() async {
    final db = await database;
    return await db.query('items');
  }

  Future<int> updateItem(int id, Map<String, dynamic> item) async {
    final db = await database;
    return await db.update('items', item, where: 'id = ?', whereArgs: [id]);
  }

  Future<int> deleteItem(int id) async {
    final db = await database;
    return await db.delete('items', where: 'id = ?', whereArgs: [id]);
  }
}
```

## 3. CRUD 기능 구현

### 3.1. Create (생성)

새로운 아이템을 데이터베이스에 추가하는 기능입니다.

```dart
Future<void> _addItem(String name) async {
  Map<String, dynamic> newItem = {'name': name};
  await DatabaseHelper().insertItem(newItem);
}
```

### 3.2. Read (조회)

데이터베이스에 저장된 모든 아이템을 조회하는 기능입니다.

```dart
Future<List<Map<String, dynamic>>> _fetchItems() async {
  return await DatabaseHelper().getItems();
}
```

### 3.3. Update (수정)

특정 아이템의 정보를 수정하는 기능입니다.

```dart
Future<void> _updateItem(int id, String name) async {
  Map<String, dynamic> updatedItem = {'name': name};
  await DatabaseHelper().updateItem(id, updatedItem);
}
```

### 3.4. Delete (삭제)

특정 아이템을 데이터베이스에서 삭제하는 기능입니다.

```dart
Future<void> _deleteItem(int id) async {
  await DatabaseHelper().deleteItem(id);
}
```

## 4. Flutter UI와 연결

이제 CRUD 기능을 Flutter UI와 연결하여 사용합니다. 기본적으로 `StatefulWidget`을 사용하여 UI를 구축하고, 사용자가 버튼을 클릭할 때마다 데이터베이스 조작이 이루어지도록 합니다.

### 4.1. `StatefulWidget` 생성

```dart
import 'package:flutter/material.dart';

class CrudExample extends StatefulWidget {
  @override
  _CrudExampleState createState() => _CrudExampleState();
}

class _CrudExampleState extends State<CrudExample> {
  List<Map<String, dynamic>> _items = [];
  final TextEditingController _controller = TextEditingController();

  @override
  void initState() {
    super.initState();
    _refreshItems();
  }

  void _refreshItems() async {
    final data = await DatabaseHelper().getItems();
    setState(() {
      _items = data;
    });
  }

  void _addItem() async {
    if (_controller.text.isEmpty) return;
    await DatabaseHelper().insertItem({'name': _controller.text});
    _controller.clear();
    _refreshItems();
  }

  void _updateItem(int id) async {
    if (_controller.text.isEmpty) return;
    await DatabaseHelper().updateItem(id, {'name': _controller.text});
    _controller.clear();
    _refreshItems();
  }

  void _deleteItem(int id) async {
    await DatabaseHelper().deleteItem(id);
    _refreshItems();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('CRUD Example')),
      body: Column(
        children: [
          Padding(
            padding: const EdgeInsets.all(8.0),
            child: TextField(
              controller: _controller,
              decoration: InputDecoration(hintText: 'Enter item name'),
            ),
          ),
          ElevatedButton(onPressed: _addItem, child: Text('Add Item')),
          Expanded(
            child: ListView.builder(
              itemCount: _items.length,
              itemBuilder: (context, index) {
                return ListTile(
                  title: Text(_items[index]['name']),
                  trailing: Row(
                    mainAxisSize: MainAxisSize.min,
                    children: [
                      IconButton(
                        icon: Icon(Icons.edit),
                        onPressed: () => _updateItem(_items[index]['id']),
                      ),
                      IconButton(
                        icon: Icon(Icons.delete),
                        onPressed: () => _deleteItem(_items[index]['id']),
                      ),
                    ],
                  ),
                );
              },
            ),
          ),
        ],
      ),
    );
  }
}
```


