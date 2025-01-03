# 🎮 Unity C# Style Guide Cheat Sheet

## 📚 Naming Conventions

- **Classes & Structs**: `PascalCase`
  ```csharp
  public class PlayerController {}
  ```

- **Methods**: `PascalCase`
  ```csharp
  public void Jump() {}  
  ```

- **Private Variables**: `_camelCase` (Prefix with underscore)
  ```csharp
  private int _playerScore;
  ```

- **Public Variables**: `camelCase` (No underscore)
  ```csharp
  public int playerScore;
  ```

- **Constants**: `UPPER_SNAKE_CASE`
  ```csharp
  private const float MAX_SPEED = 10f;
  ```

- **Enums**: `PascalCase` for names, `PascalCase` for members
  ```csharp
  public enum GameState { MainMenu, Playing, Paused }
  ```

## 🧩 Code Structure

- **File Structure**: One class per file, named after the class.
  ```csharp
  PlayerController.cs
  ```

- **Usings**: Place `using` statements at the top of the file.
  ```csharp
  using UnityEngine;
  using System.Collections;
  ```

- **Braces**: Open and close braces on a new line for multi-line methods.
  ```csharp
  public void Start() 
  {
      // code here
      // code here
  }
  ```

- **Braces**: Inline braces allowed for single line methods.
  ```csharp
  public void CompareXGreaterThanY() { return x > y; }
  ```
## 🌟 Best Practices

- **SerializeField**: Use [SerializeField] for private fields that need to be set in the Inspector.
  ```csharp
  [SerializeField] 
  private int _health = 100;
  ```

- **MagicNumbers**: Avoid using magic numbers; define them as constants.
  ```csharp
  private const int MAX_HEALTH = 100;
  ```

- **NullChecks**: Use `if (variable == null)` for null checks.
  ```csharp
  if (_enemy == null) 
  {
      // handle null
  }
  ```

## 🚀 Performance Tips

- **Caching**: Cache component references in `Awake()` or `Start()`.
  ```csharp
  private Rigidbody _rb;

  private void Awake() 
  {
    _rb = GetComponent<Rigidbody>();
  }
  ```

- **Pooling**: Use object pooling for frequently instantiated/destructed objects.
  ```csharp
  // Pseudo-code example
  ObjectPooler.Instance.SpawnFromPool("Bullet", transform.position, transform.rotation);
  ```

- **Coroutines**: Use coroutines for repeated actions with delays, such as spawning enemies at regular intervals.
  ```csharp
  private IEnumerator SpawnEnemies()
  {
      // Infinite loop to keep spawning enemies
      while(true) {
          // Code to spawn an enemy goes here
          
          // Wait for 2 seconds before the next spawn
          yield return new WaitForSeconds(2f);
      }
  }

  private void Start() 
  {
      // Start the SpawnEnemies coroutine
      StartCoroutine(SpawnEnemies());
  }
  ```
- **Spreading Out Expensive Operations**: Use coroutines to spread out expensive operations, like loading a scene, over multiple frames to avoid performance spikes.
  ```csharp
  private IEnumerator ProcessLargeTask(List<int> data) {
     for (int i = 0; i < data.Count; i++) {
         // Process data[i] here
         
         // Yield control back to Unity and continue in the next frame
         yield return null;
     }
  }
  
  private void StartProcessing() {
     StartCoroutine(ProcessLargeTask(largeDataList));
  }
  ```

## 🧹 Clean Code Principles

- **SingleResponsibility**: Each class should have one responsibility.
- **DRY (Don't Repeat Yourself)**: Avoid duplicate code by refactoring into methods or utilities.
- **KISS (Keep It Simple, Stupid)**: Simpler code is easier to maintain and understand.

## 🔗 Unity Specific

- **MonoBehaviour Methods**: Follow Unity's method execution order (Awake, Start, Update, etc.).
  ```csharp
  private void Awake() {}
  private void Start() {}
  private void Update() {}
  ```

- **Debugging**: Use `Debug.Log()`, `Debug.Assert()`, or custom tools for debugging.
  ```csharp
  Debug.Log("Player score: " + _playerScore);
  ```
