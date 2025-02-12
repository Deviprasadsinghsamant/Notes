# **C. GetX**

GetX is an easy-to-use, lightweight state management solution.

### **Key Features**

- **Minimal boilerplate**.
- **Reactive programming without Streams**.
- **Handles dependency injection and navigation**.

### **Example: Counter App using GetX**

**Step 1: Install GetX**

```yaml
dependencies:
  get: ^4.6.5
```

**Step 2: Create a Counter Controller**

```dart
import 'package:get/get.dart';

class CounterController extends GetxController {
  var count = 0.obs; // Observable variable

  void increment() {
    count++;
  }
}
```

**Step 3: Using GetX in UI**

```dart
import 'package:flutter/material.dart';
import 'package:get/get.dart';
import 'counter_controller.dart'; // Import controller

void main() {
  runApp(GetMaterialApp(home: CounterScreen()));
}

class CounterScreen extends StatelessWidget {
  final CounterController controller = Get.put(CounterController());

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("GetX Counter")),
      body: Center(
        child: Obx(() => Text("Counter: ${controller.count}", style: TextStyle(fontSize: 24))),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: controller.increment,
        child: Icon(Icons.add),
      ),
    );
  }
}
```

### **How It Works**

1. `GetxController` holds the state.
2. `.obs` makes `count` observable.
3. `Obx()` listens for changes and rebuilds UI.

✅ **Best For:** Small projects where simplicity is needed.

---
