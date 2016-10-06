RBX.Lua Support Library
=======================
A library of short, useful functions to aid in ROBLOX development. Get a [built version from ROBLOX here](https://www.roblox.com/library/516682015/Support-Library-from-F3X).

Documentation
-------------
A list of support functions provided by the module, by category:

### Tables

#### Support.FindTableOccurrences(Haystack, Needle)
Returns a table of keys where `Needle` is found in table `Haystack`.

#### Support.FindTableOccurrence(Haystack, Needle)
Returns one key where `Needle` is found in table `Haystack`, or `nil` if not found.

#### Support.IsInTable(Haystack, Needle)
Returns a boolean determining whether `Needle` is found in table `Haystack`.

#### Support.DoTablesMatch(A, B)
Returns whether the contents of tables `A` and `B` match each other identically, key-by-key.

#### Support.CloneTable(Table)
Returns a new table whose contents are identical to `Table`. **Note: Metatables are not copied over.**

#### Support.IdentifyCommonItem(Items)
Returns the common item in table `Items`, or `nil` if the contents of `Items` vary.

#### Support.ConcatTable(DestinationTable, SourceTable)
Inserts all values from `SourceTable` into `DestinationTable`, and returns `DestinationTable`. **Note: Only _values_ are inserted into `DestinationTable`; keys are not preserved.**

#### Support.ClearTable(Table)
Clears out every value in `Table`, and returns the same now-empty `Table`.

#### Support.Values(Table)
Returns a new table containing all values found in `Table`.

#### Support.Keys(Table)
Returns a new table containing all keys found in `Table`.

#### Support.CountKeys(Table)
Returns the total number of keys in table `Table`.

#### Support.Slice(Table, Start, End)
Returns a new table containing the values of `Table` from index `Start`, to index `End`, in order.

#### Support.FlipTable(Table)
Returns a new table with keys and values from table `Table` swapped.

Example:
```lua
local Table = { 'Hi', 'Hello' }
local FlippedTable = Support.FlipTable(Table)

print(Table[1]) --> Hi
print(FlippedTable.Hi) --> 1
```

#### Support.GetListMembers(List, MemberName)
Returns a table containing the values at index `MemberName` of each indexable item in table `List`.


### Numbers

#### Support.Round(Number, Places)
Returns `Number` rounded to the given number of decimal `Places`.

#### Support.Clamp(Number, Minimum, Maximum)
Returns `Number` clamped to the given `Minimum` and `Maximum` values.

Example:
```lua
print(Support.Clamp(5, 0, 3)) --> 3
print(Support.Clamp(-0.5, 0, 1)) --> 0
```


### Instances

#### Support.GetAllDescendants(Parent)
Returns a table containing all the descendants of instance `Parent`.

#### Support.GetDescendantCount(Parent)
Returns the total number of descendants within instance `Parent`.

#### Support.CloneParts(Parts)
Returns a new table containing clones of the instances in table `Parts`, with matching keys.

#### Support.GetChildOfClass(Parent, ClassName, Inherit)
Returns a child within instance `Parent` of class `ClassName`, or `nil` if not found.

If `Inherit` is `true`, class inheritance is taken into account. By default, class names must be **identical** to match.

#### Support.GetChildrenOfClass(Parent, ClassName, Inherit)
Returns a table of children within instance `Parent` of class `ClassName`.

If `Inherit` is `true`, class inheritance is taken into account. By default, class names must be **identical** to match.

#### Support.IdentifyCommonProperty(Items, Property)
Returns the common value of property `Property` across instances in table `Items`, or `nil` if the items' properties' vary.

#### Support.GetPartCorners(Part)
Returns a table containing the CFrames of corners of part `Part`. **Note: Shape is always assumed to be a rectangular prism.**


### Strings

#### Support.SplitString(String, Delimiter)
Returns the parts of string `String` after splitting it by pattern string `Delimiter`.

#### Support.Trim(String)
Returns `String` without leading or trailing spaces.


### Functions

#### Support.Call(Function, ...)
Returns a function, which calls function `Function` with arguments `...`.

Example:
```lua
Support.Call(print, 'Hi')() --> Hi
```

#### Support.ChainCall(...)
Returns a function, which when called, calls each function in `...` with the passed arguments. Each function listed in `...` receives the returned values of the previous function.

Example:
```lua
Support.ChainCall(string.upper, print)('Hello!') --> HELLO!
```


### Miscellaneous

#### Support.ScheduleRecurringTask(TaskFunction, Interval)
Calls `TaskFunction` every `Interval` seconds asynchronously. Returns a controller to stop the task, or check if it's running (`Task:Stop()`, or boolean `Task.Running`).

Example:
```lua
function PrintHi()
  print 'Hi'
end

local Task = Support.ScheduleRecurringTask(PrintHi, 0.5) --> Begins printing 'Hi' every 0.5 seconds

wait(5)
Task:Stop() --> Stops printing 'Hi' every 0.5 seconds after 5 seconds
```

#### Support.ImportServices()
Injects variables to common services into the environment in which the function was called.

Service Name | Variable Name | Different
------------ | ------------- | ---------
Workspace | Workspace |
Players | Players |
MarketplaceService | MarketplaceService |
ContentProvider | ContentProvider |
SoundService | SoundService |
UserInputService | UserInputService |
Selection | SelectionService | X
CoreGui | CoreGui |
HttpService | HttpService |
ChangeHistoryService | ChangeHistoryService |
ReplicatedStorage | ReplicatedStorage |
GroupService | GroupService |
ServerScriptService | ServerScriptService |
StarterGui | StarterGui |
RunService | RunService |

Example:
```lua
Support.ImportServices()
print(MarketplaceService:GetProductInfo(516682015).Creator.Name) --> F3X
print(GroupService:GetGroupInfoAsync(831895).Id) --> 831895
```

#### Support.AddUserInputListener(InputState, InputType, CatchAll, Callback)
Returns a connection to the requested user input event (UserInputService.Input`InputState`), and calls function `Callback(InputObject)` when the UserInputType matches `InputType`. Ignores game-processed input events, unless `CatchAll` is `true`. Also ignores keyboard input if a TextBox is currently in focus.

Example:
```lua
Support.AddUserInputListener('Began', 'Keyboard', false, function (Input)
  print(Input.KeyCode) --> Enum.KeyCode.A
end)
```

#### Support.AddGuiInputListener(Gui, InputState, InputType, CatchAll, Callback)
Returns a connection to the requested user input event in GUI instance `Gui`, and calls function `Callback(InputObject)` when the UserInputType matches `InputType`. Ignores game-processed input events, unless `CatchAll` is `true`.
