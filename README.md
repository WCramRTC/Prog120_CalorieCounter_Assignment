
# Programming 120 - Final - Calorie Counter

## Goal

You are creating a basic  calorie counting application. 
For this application you will provide a menu system that will allow
- Displaying all the calories you have eaten
- Add New Items
- Calculate your total calories eaten
- Calculate the average calories of an item you've eaten
- Display all food eaten of a certain category
- Search for a food item by name
- Exit
## Requirements

- No Compile Errors on Submission ( This means can build and run with no errors. ) 
	- 50% point dedication 
	- This doesn't mean your  project is perfect. You can still have things that don't work properly. But this means NO read squiggly errors
- Standard Header - In Comments
	- Name
	- Date
	- Assignment Name
- Submission with GitHub URL link in text box
- Comments Explaining your Code

## Expectations

For your final you will demonstrate all the skills you developed during your time in programming 1. This includes

|            |         | Topics |               |           |
| :--------: | :-----: | :----: | :-----------: | :-------: |
|   Inputs   | Outputs | Loops  |  Conditions   | Variables |
| Operations | Methods | Arrays | Linear Search |  Classes  |

--- 
## class FoodItem Class

Using the table below use it to help define your 

| Name     | Category  | Calories | Quantity | Total Calories |
| -------- | --------- | -------- | -------- | -------------- |
| Apple    | Fruit     | 95       | 1        | 95             |
| Banana   | Fruit     | 105      | 2        | 210            |
| Carrot   | Vegetable | 25       | 3        | 75             |
| Broccoli | Vegetable | 55       | 2        | 110            |
| Chicken  | Protein   | 165      | 1        | 165            |
| Beef     | Protein   | 250      | 1        | 250            |
| Rice     | Grain     | 205      | 1        | 205            |
| Bread    | Grain     | 80       | 2        | 160            |
| Milk     | Dairy     | 150      | 1        | 150            |
| Cheese   | Dairy     | 110      | 2        | 220            |

### *Fields*
- Name : string
- Category : Int
- Calories : Int
- Quantity : Int

### *Constructor*
- **public FoodItem(name, category, calories, quantity)**
- **public FoodItem()** // Default Constructor
	- This will populate the fields with
	- Name is "No Item Listed"
	- Category is -1
	- Calories is -1
	- Quantity is -1

### *Methods*

```csharp
	public double TotalCalories()
```
- // Do the calculation to return the total calories of an instance of the instanced object

```csharp
	public string CategoryName()
```
- // Write the code that takes the category number assigned at returns the proper. Here's the list
	1. Fruit
	2. Vegetable
	3. Protein
	4. Grain
	5. Dairy
	- For any other number put "No Category Chosen"

```csharp
	public string DisplayInformation();
```
- // Returns a formatted string with the items information
	- ***Use the methods you created to display Total Calories and Category***
- Example Output
```
Name: Apple
Category : Fruit
Calories : 95
Quantity : 1
Total Calorites : 95
```


---

## class Program

### *Field*
static FoodItem[] foodItems = new FoodItems[2];
	- Create an initialize your array to the size of 4

### *Methods*

### `static void Main(string[] args)`
- Only methods that should be called in main will be your Preload and Menu.
```csharp
	public static void Main(string[] args) {
		Preload();
		Menu();
	}
```

### *`static void Preload()`*
- This methods is used to populate your array with 2 items
- Select two from the provided table

###  `static void DisplayAllFoodItems()`
- Displays all the items in the FoodItem array
- Needs to use `.DisplayInformation()`
- Can use any loop of your choice

---
## Adding An Item
- You are creating 1 method, `AddItem()`, that will call 3 seperate methods.
1. A method that asks the user for the info for the new `FoodItem` object
2. A method that checks for the first empty array slot, either returns the index or -1
3. A method that will double the size of the array and populate it with the previous items

### *`static FoodItem MakeNewItem()`*
- Ask the user for a
	- Name
	- Category
		- This should be done as a list of categories
			1. Fruit
			2. Vegetable
			3. Protein
			4. Grain
			5. Dairy
		- You should validate with a try parse that the input is a valid number, and continue to ask until a proper value is entered
	- Calories
		- Validate with TryParse
	- Quantity
		- Validate with TryParse
- After all the information is added, you should then create a new Instance of `FoodItem` and return it.

### `static int FindEmptyIndex()`
- *Uses Linear Search*
- Checking for null, search your foodItems array for the first empty index
```
	foodItems[0] // Has Apple
	foodItems[1] // Has Banana
	foodItems[2] // null <---- This is first empty index, return 2
```

- If there are NO empty slots, return -1
```
	foodItems[0] // Has Apple
	foodItems[1] // Has Banana
	// ------------ End of array
	return -1
```

### `static void IncreaseArraySize()`
- If the array is full double the size the array
- Move the elements from the first array to the second
- Replace the original array with the new array


### `static void AddItem()`
- Code provided below
- If your previous 3 methods work properly when you call this method you should
	- Prompt the user for new information for their Food Item
	- Checks for an index
	- Expands the array if there is no room
	- Adds the last item
```csharp
	public static void AddItem() {

		// Ask user for item
		FoodItem newItem = MakeNewItem();
	
		// To to find last index
		int firstIndex = FindEmptyIndex()
	
		// If index is NOT found, double array size, then check again for first index
		if(firstIndex == -1) {
			IncreaseArraySize()
			firstIndex = FindEmptyIndex();
		}
	
		// Add item to first index
		foodItems[firstIndex] = newItem;

	}
```

---

Example Array for following Examples

| Name   | Category | Calories | Quantity | Total Calories |
| ------ | -------- | -------- | -------- | -------------- |
| Apple  | Fruit    | 95       | 1        | 95             |
| Banana | Fruit    | 105      | 2        | 210            |

### `static double TotalCaloriesEaten()`
- Should loop through the array and sum the total calories eaten of all items
```console
double totalCalories = TotalCaloriesEaten();
Console.WriteLine($"Your total calories are {totalCalories}");
// Result : Your total calories are 305
```


### `static double AverageCalorieEaten()`
- Should loop through your array and get the average item calorie that you ass

```console
double averageCalories = AverageCaloriesEaten();
Console.WriteLine($"Youe average calories are {averageCalories}");
// Result : Your average calories are 152.5
```

### `static void DisplayByCategory`
- Create a method that will ask the user to select a category
- You should then display all items ONLY in that category

```console
Please select a category (Fruit, Vegetable, Protein, Grain, Dairy):
Fruit

Name: Apple
Category: Fruit
Calories: 95
Quantity: 1
Total Calories: 95

Name: Banana
Category: Fruit
Calories: 105
Quantity: 2
Total Calories: 210

```

### `static void DisplayItemWithName(string foodName)`
- Ask the user for a food name
- Display the item with that name
- Otherwise display name doesn't exist
- *Uses linear search*
- Should be case insensitive ( doesn't matter if there are upper or lower cases )

```console
Please enter a food name: banana 

Name: Banana 
Category: Fruit 
Calories: 105 
Quantity: 2 
Total Calories: 210

-----

Please enter a food name: pasta 

The name 'pasta' doesn't exist.
```

### `static void Menu()`
- Create a method that Displays the full menu
- This should loop until the user chooses to exit
- Should use a switch
- Menu Options below
	- Displaying all the calories you have eaten
	- Add New Items
	- Calculate your total calories eaten
	- Calculate the average calories of an item you've eaten
	- Display all food eaten of a certain category
	- Search for a food item by name
	- Exit

```console
	Menu Options: 
	1. Display all the calories you have eaten 
	2. Add New Items 
	3. Calculate your total calories eaten 
	4. Calculate the average calories of an item you've eaten 
	5. Display all food eaten of a certain category 
	6. Search for a food item by name 
	7. Exit Please select an option (1-7):
```

---

## Rubric

| Basics           | Score  |
| ---------------- | ------ |
| Commented Header | 10     |
| URL Submission   | 10     |
| Comments         | 20     |
| ***Total***        | ***40*** |

| Class FoodItem     |   Score   |
| :----------------- | :-------: |
| Fields             |    20     |
| Constructors       |    20     |
| **Methods**        |           |
| DisplayInformation |    20     |
| Categories         |    20     |
| TotalCalories      |    20     |
| ***Total***        | ***100*** |

| Program               | Score |
| --------------------- | ----- |
| Fields                | 10    |
| **Methods**           |       |
| Preload()             | 10    |
| DisplayAllFoodItems() | 10    |
| AddItem()             | 40    |
| TotalCaloriesEaten()  | 10    |
| AverageCalorieEaten() | 20    |
| DisplayByCategory()   | 20    |
| DisplayItemWithName() | 20    |
| Menu()                | 20    |
| ***Total***               | ***160*** |

#### Reminder : If your project is submitted with compile errors your score will be divided by 50%
