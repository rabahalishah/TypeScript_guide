# TypeScript_guide
#### Typescript
its a superset of javascript.
It simply extends JS.

JS is dynamically typed its not statistically typed. Means JS already identify the inputs whether it is either a number or string. But the errors would be reduce and the code will behave expectedly we go with TS.

For Example:
```bash
function add(a, b) {
  return a + b;
}

const result = add(2, 5);

console.log(result);
// Output would be: 7
```

BUT WHAT IF I ENTER strings instead of numbers?
```bash
function add(a, b) {
  return a + b;
}

const result = add('2', '5');

console.log(result); // '25'
```

This time JS concatinate the strings instead of adding them? So whats wrong?
The problem is that no one is warning me about what this function actually supposed to do. Like in this case function is supposed to add numbers so the arguments must of number type but I intentionally entered strings and as a the results were not as expected. It should warn me on entering string instead of number.
So the solution to this problem is TS. 

So we can do something like this with TS:
```bash
function add(a: number, b:number) {
  return a + b;
}

const result = add(2, 5);

console.log(result); // now the function parameters are of number type. So on entering a string now instead of number this function will give me a warning
```

NOTE: Every type declaration is in small letters like number not Number same case for string not String


### Installation Guide
```bash
npm init 
npm install typescript --save-dev
npx tsc yourFileName.ts
```

**NOTE:** TS do not run in browser so you need to install TS compiler (tsc) This will warn us in IDE but on the time of running into browser it will first convert into JS. So by running 
npx tsc yourFileName.ts IDE will create a js version of your TS file which will run in the browser


### BASE types
// Premitve data types

For Example
```bash
let age: number;

age = 12;

let userName: string;

userName= 'John'

let state: boolean;

state = true;

// Some complex data types like arrays and obj
```

this is how you tell TS that the data type is an array of string
```bash
let hobbies : string[];

hobbies = ['gym' , 'reading bookd', 'cycling']

let records: number[];

records= [124,125,168,169]
```

### Objects

in order to create an object with specific/ unique data type of each of its key variable you can do something like below:
```bash
let person: { 
name: string; 
age: number;
};


person = {

name: 'max',
age: 12
}
```

Now if you want to store an array of objects you can do something like this of the same syntax and data type above you can do something like this:

```bash
let person: { 
name: string; 
age: number;
}[];


person = [{

name: 'max',
age: 12
},
name: 'john',
age: 19
},
name: 'Kyle',
age: 24
},

]
```

### any type
```bash
let profile: any;
```

here any is a default data types here any simply means any data type you can store in profile variable.


### Type inference
This is a feature of TS which allows you to write some less code. In this feature TS will automatically assign a data type on assigning a value. Means you dont need to explicitly define data type:

for example:
```bash
let courseName= 'The react Guide'

// Now If I will do something like this 
coursName = 123
```

I will get an error. The reason is that while defining courseName I gave it a string value. Due to inference feature TS automatically assumed that the courseName is suppoed to be a string type. Therefore, on reassingin its value with a number we will get an error.
This may be a good feature but can cause a problem sometime so in order to prevent this its always a good practice to define types in TS.

//So instead of doing this: 
```bash
let courseName='The react Guide'
```

```bash
//you should do this:
let courseName : stirng = 'The react Guide'
```


moreover If you want to assign courseName more than 2 data types you can do something like this:
```bash
let courseName: string | number | boolean = 'The react Guide'
```

this means that courseName variable could be a string, number or boolean type.


### Alias type
If you want to create a custom complex data type you can do it by using alias

for example:
```bash
type combo = {
  name: string;
  age: number;
}

let profile: combo;
```

here combo is my complex data type which is an obj type with one string variable and one number variable data type. This will help you in avoiding repeatability


### types for functions
since we know that we can define types for parameters. But we can also define types for return statement
```bash
function add(a: number, b:number): number | string {
  return a + b;
}
```


here I have assigned return a type of either number or string.

### Generics
Generics simply ensure that the type inference would be according to the input parameters

for example
```bash
function insertAtBeginning(array: any[], value: any){
  const newArray = [value, ...array]
  return newArray
  }
  
  const demoArray = [1,2,4]
  const updatedArray = insertAtBeginning(demoArray, 5)
```

here updatedArray is of any data type. As in this case the parameters are of any data type.
to make the updatedArray of the same data type as the parameters we can do so:
```bash
function insertAtBeginning<T>(array: T[], value: T){
  const newArray = [value, ...array]
  return newArray
  }
  
  const demoArray = [1,2,4]
  const updatedArray = insertAtBeginning(demoArray, 5)
```
Here T is making sure that the new array would be of the same type as parameters due to the T

## For React Functional component:
```bash
interface DndPropsType {
  title: string;
  droppableId: string;
  taskList: TaskDataType[];
  handleCreateOpenForm: () => void;
  handleOpenUpdateForm: (droppableId: string) => void;
  setTaskData: (taskData: TaskDataType) => void;
  searchValue: string;
}

const Dnd: React.FC<DndPropsType> = ({
  title,
  droppableId,
  taskList,
  handleCreateOpenForm,
  handleOpenUpdateForm,
  setTaskData,
  searchValue,
}) => {// ...Rest of the code}
```

## For axios and useState
```bash
interface ProjectData {
  id: string;
  name: string;
  description: string;
}
  const [projectsData, setProjectsData] = React.useState<AxiosResponse | null | void>();
 async function fetchData() {
    try {
      const response: AxiosResponse<ProjectData[]> = await axios.get<
        ProjectData[]
      >('http://localhost:3000/projects');
      console.log("Company's Data: ", response);
      if (response.data.length === 0) setEmptyObj(true);
      setProjectsData(response);
    } catch (err) {
      console.log(err);
      throw new Error('Something went wrong!');
    }
  }
```

# For useContextHook:
```bash
interface ContextProps {
  boardListName: string;
  setBoardListName: (name: string) => void;
  taskData: TaskDataType;
  setTaskData: (data: TaskDataType) => void;
  toDoList: TaskDataType[];
  updatedToDoList: (list: TaskDataType[]) => void;
  completeList: TaskDataType[];
  updatedCompleteList: (list: TaskDataType[]) => void;
  inProgressList: TaskDataType[];
  updateInProgressList: (list: TaskDataType[]) => void;
  reviewList: TaskDataType[];
  updateReviewList: (list: TaskDataType[]) => void;
}
const Board = () => {
  const {
    boardListName,
    setBoardListName,
    taskData,
    setTaskData,
    toDoList,
    updatedToDoList,
    completeList,
    updatedCompleteList,
    inProgressList,
    updateInProgressList,
    reviewList,
    updateReviewList,
  } = useContextHook() as ContextProps; //<--- this is how you do
  return({
  //...rest if the code
})
```

## For Functions
type updateListFunction = (items: TaskDataType[]) => void;

## For making a property optional 
export interface TaskDataType {
  assignee: teamMemberType | undefined;
  description: string;
  dueDate: string;
  id: string;
  name: string;
  priority: priority | undefined;
  reporter: teamMemberType | undefined;
  startDate: string;
  taskStatus: string;
  labels: string;
  department: string;
  category: string;
  teamMember?: teamMemberType; // <------- Making teamMember optional
}

