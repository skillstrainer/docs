# Assignments for Mobile Dev Candidates

## Assignment #1:

### Objective

Write a function that receives 2 objects A and B, calculates their diff and returns an object that represents the differences between the 2 objects in the following manner:

1. If object A contains keys that object B doesn't, then the resultant object should have a key called `__exists_in_a` which would be an object containing all those key value pairs.
2. If object A contains a key that object B does but the values are different, then the resultant object should have an object against the same key which contains two keys, namely, `__value_in_a` and `__value_in_b` that hold the value of that key in object A and object B respectively.
3. If object A contains a key that object B does but the values are both objects, then the resultant object should have a recursive comparison of both the objects against the same key.
4. If object A contains a key that object B does and the values are both arrays, then the resultant object should have an object against the same key which contains three keys, namely, `__items_in_a`, `__items_in_b` and `__common_items`. As the names suggest, all these keys should hold an array value where `__items_in_a` contains items exclusively in object A, `__items_in_b` contains items exclusively in object B and `__common_items` contains items that are in both the objects.
   Items in the array would not be of array type. If the arrays contain items of object type, then the items can be identified as the same if their `id` values are the same. The objects should then be recursively compared in the same manner.

For example:
Let's say that object A has the following structure:

```json
{
  "name": "Peter",
  "reads": [
    {
      "id": 1,
      "name": "Book A",
      "published_at": "2023-01-02T00:00:00.00Z"
    },
    {
      "id": 2,
      "name": "Book B",
      "published_at": "2023-01-03T00:00:00.00Z"
    }
  ],
  "tags": {
    "smokes": true,
    "bachelor": true,
    "height": 6.4
  }
}
```

and object B has the following structure:

```json
{
  "name": "Davidson",
  "reads": [
    {
      "id": 3,
      "name": "Book A1",
      "published_at": "2023-01-02T00:00:00.00Z"
    },
    {
      "id": 2,
      "name": "Book B",
      "published_at": "2023-01-04T00:00:00.00Z"
    }
  ],
  "tags": {
    "smokes": false,
    "bachelor": true,
    "weight": 70
  }
}
```

then the resultant object would be:

```json
{
  "name": {
    "__value_in_a": "Peter",
    "__value_in_b": "Davidson"
  },
  "reads": {
    "__items_in_a": [
      {
        "id": 1,
        "name": "Book A",
        "published_at": "2023-01-02T00:00:00.00Z"
      }
    ],
    "__items_in_b": [
      {
        "id": 3,
        "name": "Book A1",
        "published_at": "2023-01-02T00:00:00.00Z"
      }
    ],
    "__common_items": [
      {
        "id": 2,
        "name": "Book B",
        "published_at": {
          "__value_in_a": "2023-01-03T00:00:00.00Z",
          "__value_in_b": "2023-01-04T00:00:00.00Z"
        }
      }
    ]
  },
  "tags": {
    "smokes": {
      "__value_in_a": true,
      "__value_in_b": false
    },
    "bachelor": true,
    "__exists_in_a": {
      "height": 6.4
    },
    "__exists_in_b": {
      "weight": 70
    }
  }
}
```

### Deliverables:

1. Source code of the function fulfilling all the features and functional requirements.
2. Unit tests covering all functionalities.

### Evaluation Criteria:

1. Adherence to the assignment brief and completion of all requirements.
2. Code quality, readability, and organization.

## Assignment #2

### Objective

Create a React component that implements a slider with the following features and functionalities:

### Features:

1. **MinMax Values**: The slider should have a minimum and maximum value that can be set via props.
2. **Step Value**: The slider should move in increments defined by a `step` prop.
3. **Default Value**: The slider should accept a `defaultValue` prop that sets its initial value.
4. **Dynamic Labels**: Display the current value of the slider above the thumb (draggable element). The label should update dynamically as the thumb moves.
5. **Draggable**: The slider thumb should be draggable but should snap to the nearest value when released.
6. **Two-way Binding**: The component should update its value when receiving a new `value` prop. It should also notify the parent component when the slider value changes, preferably through a callback function prop like `onChange`.
7. **Disabled State**: Add a prop called `disabled` that, when set to true, disables the slider from any interaction.
8. **Styling**: The slider should accept custom styles via a `style` prop, and its look should be easily customizable through CSS classes.
9. **Accessibility**: Make sure the slider is accessible through keyboard events (e.g., using arrow keys to move the thumb).

### Functional Requirements:

1. Use the latest version of React and create the component as a functional component using hooks.
2. Manage the component's state effectively, ensuring smooth performance.
3. You must write the component in JSX and make use of React's event system for handling events.

### Example Usage:

```jsx
<Slider
  min={0}
  max={100}
  step={1}
  defaultValue={50}
  onChange={(value) => console.log("Slider value:", value)}
  disabled={false}
  style={{ backgroundColor: "lightgrey" }}
/>
```

### Deliverables:

1. Source code of the React Slider component fulfilling all the features and functional requirements.
2. Documentation outlining how to use the component, how to run tests, and any other information required for a developer to use the component.

### Evaluation Criteria:

1. Adherence to the assignment brief and completion of all requirements.
2. Code quality, readability, and organization.
3. Usability and accessibility of the Slider component.
4. Quality of documentation.

## Deliverables

Submit the above mentioned deliverables in a zip with the following folder structure to **tech@skillstrainer.in**:

- /assignment_1
  - object_diff_calculator.js (or .ts)
  - test_cases.js (or .ts)
- /assignment_2
  - /SliderComponent
    - index.jsx (or .tsx)
    - index.css
  - SliderComponent_Documentation.md
