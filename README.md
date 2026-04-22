# Password Generator Project Documentation

## Overview
This is a Java-based password generator application that provides features for generating secure passwords, checking password strength, displaying useful information, and managing saved passwords. The application is interactive and runs via command line.

## Project Structure
The project consists of the following files and directories:

### Source Files (`src/` directory)
- **Main.java**: The entry point of the application. It initializes the Scanner for user input and starts the main loop.
- **Generator.java**: Contains the core logic for the password generator. Handles user interaction, password generation, strength checking, and password storage.
- **Alphabet.java**: Defines the character sets (uppercase, lowercase, numbers, symbols) used for password generation.
- **CryptographyManager.java**: Handles encryption and decryption operations for secure password storage.
- **KeyManager.java**: Manages cryptographic keys used in the encryption process.
- **Password.java**: Represents a password object with methods for strength calculation and string representation.
- **PasswordStorage.java**: Provides functionality to save and retrieve encrypted passwords with labels.
- **SecureRandomUtil.java**: Utility class for generating secure random numbers.
- **GeneratorTest.java**: Contains JUnit tests for validating the functionality of various components.


## Detailed File Explanations

### Main.java
```java
import java.util.Scanner;

public class Main {
    public static final Scanner keyboard = new Scanner(System.in);

    public static void main(String[] args) {
        Generator generator = new Generator(keyboard);
        generator.mainLoop();
        keyboard.close();
    }
}
```
- **Purpose**: Serves as the application's entry point.
- **Process**:
  1. Creates a shared Scanner object for reading user input from System.in.
  2. Instantiates a Generator object with the Scanner.
  3. Calls the mainLoop() method to start the interactive session.
  4. Closes the Scanner when the program ends.

### Generator.java
This file contains the main application logic with several key methods:

- **Constructor**: Initializes the Generator with a Scanner and creates a PasswordStorage instance.
- **mainLoop()**: Displays the main menu and handles user choices in a loop until quit.
- **requestPassword()**: Guides the user through password generation options and creates the password.
- **checkPassword()**: Evaluates the strength of a user-provided password.
- **printUsefulInfo()**: Displays password security best practices.
- **retrievePassword()**: Allows retrieval of saved passwords by label.
- **GeneratePassword(int length)**: Creates a random password of specified length using the configured alphabet.

**Password Generation Process**:
1. User selects character types (uppercase, lowercase, numbers, symbols).
2. User specifies password length.
3. A new Generator instance is created with the selected options.
4. Secure random indices are generated to select characters from the alphabet.
5. Characters are appended to build the password string.
6. The password is displayed and optionally saved.

### Alphabet.java
Defines static string constants for different character sets:
- UPPERCASE_LETTERS: "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
- LOWERCASE_LETTERS: "abcdefghijklmnopqrstuvwxyz"
- NUMBERS: "0123456789"
- SYMBOLS: "!@#$%^&*()-_=+[]{}|;:,.<>?"

Provides a constructor to build a custom alphabet based on user selections.

### CryptographyManager.java
Handles encryption/decryption using AES algorithm:
- Uses a secret key for symmetric encryption.
- Provides methods to encrypt and decrypt strings.

### KeyManager.java
Manages the generation and storage of cryptographic keys:
- Generates a secret key for AES encryption.
- Provides methods to retrieve the key.

### Password.java
Represents a password with strength calculation:
- Stores the password string.
- calculateScore(): Analyzes password strength based on length, character variety, etc.
- toString(): Returns the password string.

### PasswordStorage.java
Manages encrypted password storage:
- savePassword(String label, String password): Encrypts and saves password with a label.
- getPassword(String label): Retrieves and decrypts password by label.
- listLabels(): Displays all saved password labels.

### SecureRandomUtil.java
Provides secure random number generation:
- Uses SecureRandom for cryptographically strong random numbers.
- nextInt(int bound): Returns a secure random integer within the specified range.

### GeneratorTest.java
JUnit test class with test methods:
- test1(): Verifies Password object creation.
- test2(), test3(): Test Alphabet configurations.
- test4(), test5(): Validate Generator alphabet setup.

## Build and Run Process

1. **Setup**:
   - Determines script directory.
   - Creates `bin/` directory if it doesn't exist.
   - Locates javac and java executables (first tries bundled JDK, then system PATH).

2. **Compilation**:
   - Finds all .java files in `src/` (excluding *Test.java).
   - Compiles them to `bin/` using javac.

3. **Execution**:
   - Runs the Main class with java, using `bin/` as classpath.

### Manual Process
If running manually:
1. Compile: `javac -d bin src/*.java`
2. Run: `java -cp bin Main`
java -cp "Password Generator/bin" Main

## Application Workflow
1. Program starts and displays welcome message and menu.
2. User selects an option (1-5).
3. Based on choice:
   - 1: Password generation wizard.
   - 2: Password strength checker.
   - 3: Display security information.
   - 4: Retrieve saved password.
   - 5: Exit program.
4. After each action (except quit), menu redisplays.
5. Loop continues until user chooses to quit.

## Security Features
- Uses SecureRandom for password generation.
- AES encryption for password storage.
- Follows password security best practices.
- No plaintext password storage.

## Dependencies
- Java 17 or higher.
- JUnit 5 (for tests, not included in runtime).

## Notes
- The application is designed for command-line interaction.
- Passwords are generated using cryptographically secure random numbers.
- Saved passwords are encrypted before storage.
- The bundled JDK was removed to reduce project size; system JDK is used instead.
