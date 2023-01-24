** Please note that these are only recommendations based on those provided by Microsoft.
Consistency is key.
Don’t overengineer it by attempting to account for every single edge case from the start.

Formatting rules
Allman style: which places the opening curly braces on a new line.
// EXAMPLE: Allman or BSD style puts opening brace on a new line.

void DisplayMouseCursor(bool showMouse) 
{
     if (!showMouse)
     {
          Cursor.lockState = CursorLockMode.Locked;
          Cursor.visible = false;
     }
}
K&R style, or “one true brace style: which keeps the opening brace on the same line as the previous header.
// EXAMPLE: K&R style puts opening brace on the previous line.

void DisplayMouseCursor(bool showMouse){
     if (!showMouse) {
          Cursor.lockState = CursorLockMode.Locked;
          Cursor.visible = false;
     }
}

For improving readability
Add spaces to decrease code density: The extra whitespace can give a sense of visual separation between parts of a line.
// EXAMPLE: Add spaces to make lines easier to read.
for (int i = 0; i < 100; i++) { DoSomething(i); }

// AVOID: No spaces
for(int i=0;i<100;i++){DoSomething(i);}

Use a single space after a comma, between function arguments.
// EXAMPLE: Single space after comma between arguments
CollectItem(myObject, 0, 1);

// AVOID:
CollectItem(myObject,0,1);

Don’t add a space after the parenthesis and function arguments.
// EXAMPLE: No space after the parenthesis and function arguments 
DropPowerUp(myPrefab, 0, 1);

// AVOID:
DropPowerUp( myPrefab, 0, 1 );

Don’t use spaces between a function name and parenthesis.
// EXAMPLE: Omit spaces between a function name and parenthesis.
DoSomething()

// AVOID:
DoSomething ()

Avoid spaces inside brackets.
// EXAMPLE: Omit spaces inside brackets.
x = dataArray[index];

// AVOID:
x = dataArray[ index ];

Use a single space before flow control conditions: Add a space between the flow comparison operator and the parentheses.
// EXAMPLE: Space before condition; separate parentheses with a space
while (x == y)

// AVOID:
while(x==y)

Use a single space before and after comparison operators.
// EXAMPLE: Space before condition; separate parentheses with a space
if (x == y)

// AVOID:
if (x==y)

Naming conventions
General Convention
Don’t abbreviate names.
Single letter variables are fine for loops and math expressions.
Use one variable declaration per line 
If your class is called Player, you don’t need to create member variables called Player Score or Player Target. Trim them down to Score or Target.
avoid too many prefixes or special encoding.
prefix private member variables with an underscore (_)
prefix interface names with a capital “I”
prefix the event raising method (in the subject) with “On” Some style guides use prefixes for private member variables (m_), constants (k_), or static variables (s_), so the name reveals more about the variable.
// EXAMPLE: Prefix interface names with a capital “I”
public interface IDamageable<T>
{
    void Damage(T damageTaken);
}


// EXAMPLE: Raising an event if you have subscribers
public void OnDoorOpened()
{
    DoorOpened?.Invoke();
}

Variable
try to attribute clear and descriptive nouns to their names.
Pascal case for public fields, enums, classes, and methods
Camel case for private variables
private int _elapsedTimeInDays;

// Use [SerializeField] attribute if you want to display a private field in Inspector.
// Booleans ask a question that can be answered true or false.
[SerializeField] private bool _isPlayerDead;

// This groups data from the custom PlayerStats class in the Inspector.
[SerializeField] private PlayerStats _stats;

// This limits the values to a Range and creates a slider in the Inspector.
[Range(0f, 1f)] [SerializeField] private float _rangedStat;

// A tooltip can replace a comment on a serialized field and do double duty.
[Tooltip("This is another statistic for the player.")]
[SerializeField] private float _anotherStat;

// the private backing field
private int _maxHealth;

// read-only, returns backing field
public int MaxHealthReadOnly => _maxHealth;

// equivalent to:
// public int MaxHealth { get; private set; }

// explicitly implementing getter and setter
public int MaxHealth
{
    get => _maxHealth;
    set => _maxHealth = value;
}

// write-only (not using backing field)
public int Health { private get; set; }

// write-only, without an explicit setter
public void SetMaxHealth(int newMaxValue) => _maxHealth = newMaxValue;

// auto-implemented property without backing field
public string DescriptionName { get; set; } = "Fireball";

Boolean
prefix booleans with a verb for variables that must indicate a true or false value.
Often they are the answer to a question such as, is the player running? Is the game over? Prefix them with a verb to clarify their meaning. This is often paired with a description or condition, e.g., isPlayerDead, isWalking, hasDamageMultiplier,etc.

Method
Since methods perform actions, a good rule of thumb is to start their names with a verb and add context as needed, e.g., GetDirection, FindTarget, and so on, based on the return type. If the method has a bool return type, it can also be framed as a question.
Much like boolean variables themselves, prefix methods with a verb if they return a true-false condition. This phrases them in the form of a question, e.g., IsGameOver, HasStartedTurn.
// Methods start with a verb.
public void SetInitialPosition(float x, float y, float z)
{
    transform.position = new Vector3(x, y, z);
}

// Methods ask a question when they return bool.
public bool IsNewPosition(Vector3 newPosition)
{
    return (transform.position == newPosition);
}

Event
we name the event with a verb phrase, similar to a method. Choose a name that communicates the state change accurately. Use the present or past participle to indicate events “before” or “after.” For instance, specify OpeningDoor for an event before opening a door and DoorOpened for an event afterward.
// event before
public event Action OpeningDoor;

// event after
public event Action DoorOpened;

//Extra Sample
public event Action<int> PointsScored;
public event Action<CustomEventArgs> ThingHappened;
 
// These are event raising methods, e.g. OnDoorOpened, OnPointsScored, etc.
public void OnDoorOpened()
{
    DoorOpened?.Invoke();
}

public void OnPointsScored(int points)
{
    PointsScored?.Invoke(points);
}
// This is a custom EventArg made from a struct.
public struct CustomEventArgs
{
    public int ObjectID { get; }
    public Color Color { get; }

    public CustomEventArgs(int objectId, Color color)
    {
        this.ObjectID = objectId;
        this.Color = color;
    }
}

Don’t formalize everything!
Just how comprehensive your style guide should be depends on your situation. 
It’s up to your team to decide if they want their guide to set rules for more abstract, intangible concepts. 
This could include rules for using namespaces, breaking down classes, or implementing directives like the 
#region directive (or not). 
While #region can help you collapse and hide sections of code in C# files, making large files more manageable, it’s also an example of something that many developers consider to be code smells or anti-patterns. 
Therefore, you might want to avoid setting strict standards for these aspects of code styling. Not everything needs to be outlined in the guide – sometimes it’s enough to simply discuss and make decisions as a team.

Clarity above all else
Use fewer arguments: Arguments can increase the complexity of your method.
Avoid excessive overloading: If you do overload a method, prevent confusion by making sure that each method signature has a distinct number of arguments.
Avoid side effects: A method only needs to do what its name advertises. Avoid modifying anything outside of its scope. 
Pass in arguments by value instead of reference when possible.
So, when sending back results via the out or ref keyword, verify that’s the one thing you intend the method to accomplish.
