# 🧬 **PE Zero Imports Project**

## 📌 **Overview**

This project demonstrates how a **Windows Portable Executable (PE)** can be built with **zero static imports** by **manually resolving Windows APIs at runtime**.

Instead of relying on the **Import Address Table (IAT)**, the program traverses **internal PE data structures** and the **Process Environment Block (PEB)** to locate modules and resolve exported functions dynamically.

The goal of this project is **educational**, focusing on understanding:

- **PE file format internals**
- **Import resolution mechanisms**
- **Export table parsing**
- **Linked list traversal in the PEB**
- **Manual implementation of `GetModuleHandle` and `GetProcAddress`**

---

## 🎯 **Features**

- ✔️ **No static imports (empty IAT)**
- ✔️ **Manual traversal of the PEB module list**
- ✔️ **Custom `GetModuleHandle` implementation**
- ✔️ **Custom `GetProcAddress` implementation**
- ✔️ **Direct parsing of the PE Export Directory**
- ✔️ **Optional XOR string obfuscation**
- ✔️ **Dynamic API resolution at runtime**
- ✔️ **Uses only low-level Windows data structures**

---

## 🗂️ **Project Structure**
```bash
/
├── PEstructs.h # PE and Windows internal structure definitions
├── helpers.h # Function declarations and utilities
├── helpers.cpp # Manual API resolution logic (PEB + Export parsing)
└── implant.cpp # Main program logic (entry point)

---

## 🧩 **File Descriptions**

### **PEstructs.h**
Contains custom definitions for:
- **PE headers**
- **Export directory structures**
- **PEB and loader structures**

> Used to **avoid including standard Windows headers** that introduce imports.

---

### **helpers.h**
Declares:
- **Custom `hlpGetModuleHandle`**
- **Custom `hlpGetProcAddress`**
- **Utility routines for string comparison and parsing**

---

### **helpers.cpp**
Implements:
- **PEB traversal to locate loaded modules**
- **Export table parsing to locate function addresses**
- **Manual API resolution logic**

---

### **implant.cpp**
Main program file:
- **Calls manually resolved APIs**
- **Demonstrates runtime function resolution**
- **Avoids static imports entirely**

---

## ⚙️ **How It Works (High-Level)**

1. The program **reads the PEB** to obtain the loaded module list  
2. It **searches for the desired DLL** (e.g., `kernel32.dll`)  
3. It **parses the DLL’s Export Directory**  
4. It **finds function addresses** by name or ordinal  
5. The function is **called via a function pointer**  
6. The **IAT remains empty → zero imports**

---

## 🧪 **Verification**

The compiled binary can be verified using:

- **PE-bear**
- **CFF Explorer**
- **PE Studio**

### **Expected Result**
- **Import Address Table is empty**
- **No visible API strings**
- **Functions resolved only at runtime**

---

## 📚 **Learning Objectives**

This project demonstrates practical usage of:

- **Arrays** (export tables, name tables)
- **Linked lists** (PEB loader list)
- **Pointers and RVA calculations**
- **Binary / linear search**
- **Runtime symbol resolution**
- **XOR-based string obfuscation**

---

## ⚠️ **Disclaimer**

This project is intended **strictly for educational and research purposes** to understand the **Windows PE format** and **dynamic linking internals**.

🚫 **Do NOT use this code in unauthorized or malicious environments.**

---

## 👨‍💻 **Authors**

- **M Gulraiz Khan**
- **Haider Mustafa**
