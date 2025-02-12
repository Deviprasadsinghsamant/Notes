# **📡 Networking & API Integration in Flutter**

Fetching data from the internet is essential for most apps. Flutter provides networking capabilities using the **http package** and **Dio package** to make API calls, handle JSON data, and manage errors efficiently.

---

## **🔹 1. Setting Up HTTP Package**

The `http` package allows Flutter to perform network requests like **GET, POST, PUT, DELETE**.

### **Step 1: Add `http` dependency**

Add this line to your `pubspec.yaml` file:

```yaml
dependencies:
  http: ^0.13.6
```

Then, run:

```sh
flutter pub get
```

---

## **🔹 2. Making API Calls**

### **📌 GET Request (Fetching Data)**

A **GET request** retrieves data from a server.

#### **👨‍💻 Example: Fetching Data from a Fake API**

```dart
import 'dart:convert';  // For JSON parsing
import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;

void main() {
  runApp(MaterialApp(home: ApiExampleScreen()));
}

class ApiExampleScreen extends StatefulWidget {
  @override
  _ApiExampleScreenState createState() => _ApiExampleScreenState();
}

class _ApiExampleScreenState extends State<ApiExampleScreen> {
  List<dynamic> users = []; // Stores fetched data

  // Function to fetch data from API
  Future<void> fetchData() async {
    final response = await http.get(Uri.parse("https://jsonplaceholder.typicode.com/users"));

    if (response.statusCode == 200) {
      setState(() {
        users = jsonDecode(response.body); // Convert JSON response to a List
      });
    } else {
      print("Failed to load data");
    }
  }

  @override
  void initState() {
    super.initState();
    fetchData(); // Fetch data when screen loads
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("API Example")),
      body: users.isEmpty
          ? Center(child: CircularProgressIndicator()) // Show loader while fetching data
          : ListView.builder(
              itemCount: users.length,
              itemBuilder: (context, index) {
                return ListTile(
                  title: Text(users[index]["name"]),
                  subtitle: Text(users[index]["email"]),
                );
              },
            ),
    );
  }
}
```

✅ **What’s Happening Here?**

1. **`http.get()`** fetches data from an API.
2. **`jsonDecode(response.body)`** converts JSON to a List.
3. **`setState()`** updates UI when data is fetched.
4. **`ListView.builder()`** displays fetched data.

---

### **📌 POST Request (Sending Data)**

A **POST request** sends data to the server.

#### **👨‍💻 Example: Sending Data to an API**

```dart
Future<void> sendData(String name, String email) async {
  final response = await http.post(
    Uri.parse("https://jsonplaceholder.typicode.com/users"),
    headers: {"Content-Type": "application/json"},
    body: jsonEncode({"name": name, "email": email}),
  );

  if (response.statusCode == 201) {
    print("Data sent successfully: ${response.body}");
  } else {
    print("Failed to send data");
  }
}

// Call this function: sendData("John Doe", "john@example.com");
```

✅ **What’s Happening Here?**

1. **`http.post()`** sends data to the server.
2. **`jsonEncode()`** converts a Dart object to JSON.
3. **Headers define JSON format.**
4. **201 status code** indicates successful data submission.

---

## **🔹 3. Parsing JSON Data**

JSON (JavaScript Object Notation) is the standard format for API responses.

### **📌 Example JSON Response**

```json
{
  "id": 1,
  "name": "John Doe",
  "email": "john@example.com"
}
```

We can convert this JSON into a Dart model.

### **👨‍💻 Example: Parsing JSON into a Dart Model**

```dart
class User {
  final int id;
  final String name;
  final String email;

  User({required this.id, required this.name, required this.email});

  // Convert JSON to Dart Object
  factory User.fromJson(Map<String, dynamic> json) {
    return User(
      id: json['id'],
      name: json['name'],
      email: json['email'],
    );
  }
}

// Usage:
// User user = User.fromJson(jsonResponse);
```

✅ **Why Use a Model?**

- **Better code structure.**
- **Easier debugging.**
- **Type safety.**

---

## **🔹 4. Error Handling in API Calls**

Handling API errors ensures a better user experience.

### **Common Errors**

|Error Type|Cause|Solution|
|---|---|---|
|`400 Bad Request`|Invalid request|Check request data|
|`401 Unauthorized`|No authentication|Use valid API key|
|`404 Not Found`|Incorrect API endpoint|Verify API URL|
|`500 Server Error`|Server issue|Retry later|

### **👨‍💻 Example: Handling Errors**

```dart
Future<void> fetchDataWithErrorHandling() async {
  try {
    final response = await http.get(Uri.parse("https://jsonplaceholder.typicode.com/users"));

    if (response.statusCode == 200) {
      print("Data fetched successfully!");
    } else {
      throw Exception("Failed to load data: ${response.statusCode}");
    }
  } catch (e) {
    print("Error: $e");
  }
}
```

✅ **What’s Happening Here?**

1. **`try-catch`** handles errors.
2. **Throws an exception** if response is not **200 OK**.

---

## **🔹 5. Using Dio Package for Networking**

[Dio](https://pub.dev/packages/dio) is a more advanced HTTP client with:

- **Interceptors (Modify requests globally)**
- **File Uploads**
- **Timeouts & Error Handling**

### **Step 1: Add `dio` dependency**

Add this to `pubspec.yaml`:

```yaml
dependencies:
  dio: ^5.0.0
```

Run:

```sh
flutter pub get
```

### **👨‍💻 Example: Using Dio to Fetch Data**

```dart
import 'package:dio/dio.dart';

void fetchDataWithDio() async {
  try {
    final dio = Dio();
    final response = await dio.get("https://jsonplaceholder.typicode.com/users");

    if (response.statusCode == 200) {
      print(response.data); // Print response data
    }
  } catch (e) {
    print("Error: $e");
  }
}
```

✅ **Why Use Dio?**

- **Faster requests** than `http`
- **Built-in error handling**
- **Easier JSON conversion**

---

# **Layman’s Section 📖**

### **Imagine This:**

1. **GET Request is like searching on Google.** 🌍
    
    - You type "Weather today".
    - Google **fetches** data and shows results.
2. **POST Request is like submitting a feedback form.** ✉️
    
    - You fill your name & email.
    - Click **Submit**, and your data is **sent** to the server.
3. **JSON Parsing is like converting a train ticket into a readable format.** 🎟️
    
    - Ticket machine prints a **code**.
    - You **decode it** to understand your seat and train info.
4. **Error Handling is like checking your WiFi connection.** 📶
    
    - No internet? Error **"Check your connection"** is displayed.

---

# **Final Summary 📌**

|Feature|What It Does|Example|
|---|---|---|
|`http.get()`|Fetch data from API|Get user details|
|`http.post()`|Send data to API|Submit form data|
|`jsonDecode()`|Convert JSON to Dart object|Parse user details|
|`try-catch`|Handle errors|Show error message if request fails|
|`Dio`|Advanced API client|Faster networking|

Would you like me to explain anything in more detail? 😊🚀