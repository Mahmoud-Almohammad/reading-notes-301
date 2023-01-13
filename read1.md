# Component-Based Architecture

Component-based architecture focuses on the decomposition of the design into individual functional or logical components that represent well-defined communication interfaces containing methods, events, and properties. It provides a higher level of abstraction and divides the problem into sub-problems, each associated with component partitions.

Component-oriented software design has many advantages over the traditional object-oriented approaches such as −

- Reduced time in market and the development cost by reusing existing components.

- Increased reliability with the reuse of the existing components.

## What is a Component?

A component is a modular, portable, replaceable, and reusable set of well-defined functionality that encapsulates its implementation and exporting it as a higher-level interface.

## Views of a Component

A component can have three different views − object-oriented view, conventional view, and process-related view.

### Object-oriented view

A component is viewed as a set of one or more cooperating classes. Each problem domain class (analysis) and infrastructure class (design) are explained to identify all attributes and operations that apply to its implementation.

### Conventional view

It is viewed as a functional element or a module of a program that integrates the processing logic.

### Process-related view

In this view, instead of creating each component from scratch, the system is building from existing components maintained in a library.

## Characteristics of Components

1. Reusability

2. Replaceable

3. Not context specific

4. Extensible

5. Encapsulated

6. Independent

## Principles of Component−Based Design

A component-level design can be represented by using some intermediary representation (e.g. graphical, tabular, or text-based) that can be translated into source code.

- The software system is decomposed into reusable, cohesive, and encapsulated component units.

- Each component has its own interface that specifies required ports and provided ports; each component hides its detailed implementation.

- A component should be extended without the need to make internal code or design modifications to the existing parts of the component.

- Depend on abstractions component do not depend on other concrete components, which increase difficulty in expendability.

- Connectors connected components, specifying and ruling the interaction among components. The interaction type is specified by the interfaces of the components.

- Components interaction can take the form of method invocations, asynchronous invocations, broadcasting, message driven interactions, data stream communications, and other protocol specific interactions.

- For a server class, specialized interfaces should be created to serve major categories of clients. Only those operations that are relevant to a particular category of clients should be specified in the interface.

- A component can extend to other components and still offer its own extension points. It is the concept of plug-in based architecture. This allows a plugin to offer another plugin API.

## Conducting Component-Level Design

Recognizes all design classes that correspond to the problem domain as defined in the analysis model and architectural model.

- Recognizes all design classes that correspond to the infrastructure domain.

- Describes all design classes that are not acquired as reusable components, and specifies message details.

- Identifies appropriate interfaces for each component and elaborates attributes and defines data types and data structures required to implement them.

- Describes processing flow within each operation in detail by means of pseudo code or UML activity diagrams.

- Describes persistent data sources (databases and files) and identifies the classes required to manage them.

- Develop and elaborates behavioral representations for a class or component. This can be done by elaborating the UML state diagrams created for the analysis model and by examining all use cases that are relevant to the design class.

- Elaborates deployment diagrams to provide additional implementation detail.

- Demonstrates the location of key packages or classes of components in a system by using class instances and designating specific hardware and operating system environment.

- The final decision can be made by using established design principles and guidelines. Experienced designers consider all (or most) of the alternative design solutions before settling on the final design model.

## For full source Read [Component-Based Architecture][1]

***

# What is “Props” and how to use it in React?

## What is Props?

**React is a component-based library** that divides the UI into little reusable pieces. In some cases, those components need to communicate (send data to each other) and the way to pass data between components is by using **props**.

**“Props” is a special keyword in React, which stands for properties and is being used for passing data from one component to another.**

**But the important part here is that data with props are being passed in a uni-directional flow. (one way from parent to child)**

Furthermore, **props data is read-only**, which means that data coming from the parent **should not** be changed by child components.

OK now let’s see how to use Props with an example…

## Using Props in React

1. Firstly, define an attribute and its value(data)

2. Then pass it to child component(s) by using Props

3. Finally, render the Props Data

So in this example, we have a ParentComponent including another component (child):

    class ParentComponent extends Component {  
    render() {
        return (
        <h1>
            I'm the parent component.
            <ChildComponent />
        </h1>
        );
    }
    }

And this is our ChildComponent:

    const ChildComponent = () => {  
    return <p>I'm the 1st child!</p>; 
    };

The problem here is that when we call the ChildComponent multiple times:

    class ParentComponent extends Component {  
    render() {
        return (
        <h1>
            I'm the parent component.
            <ChildComponent />
            <ChildComponent />
            <ChildComponent />
        </h1>
        );
    }
    }

It always renders the same string again and again:

![example](https://miro.medium.com/max/828/1*rzX4l1-rJn4c4_yeqooFbQ.webp)

But what we like to do here is to get dynamic outputs, because each child component may have different data, and let’s see how we can solve this issue by using props…

### 1st Step: Defining Attribute & Data

We can define our own attributes & assign values with interpolation { } like this:

    <ChildComponent text={“I’m the 1st child”} />

Now the ChildComponent has a property and a value. Next, we need to pass it via Props.

### 2nd Step: Passing Data using Props

OK, now let’s take the “I’m the 1st child!” string and pass it by using props.

Passing props is very simple. Like we pass arguments to a function, we pass props into a React component and props bring all the necessary data like this:

    const ChildComponent = (props) => {  
    return <p>I'm the 1st child!</p>; 
    };

### Final Step: Rendering Props Data

Alright so far, we have created an attribute and its value, then we passed it through props but we still can’t see it because we haven’t rendered it yet.

But before render the prop, let's first log props to console and see what it shows:

    console.log(props);
![the result of log the prop](https://miro.medium.com/max/828/1*adfjNBKTxR6kf8xJLyzquA.webp)

As we can see, Props returns back an object. In JavaScript, we can access object elements with dot(.) notation. So, let’s render our text property with an interpolation:

    const ChildComponent = (props) => {  
    return <p>{props.text}</p>; 
    };

![final result for this example](https://miro.medium.com/max/828/1*UuipOqB2yPyC1JPB8MTxpQ.webp)

And that’s it! We’ve achieved to render the data coming from the parent component.

Before closing, let’s do the same for other child components:

    class ParentComponent extends Component {  
    render() {
        return (
        <h1>
            I'm the parent component.
            <ChildComponent text={"I'm the 1st child"} />
            <ChildComponent text={"I'm the 2nd child"} />
            <ChildComponent text={"I'm the 3rd child"} />
        </h1>
        );
    }
    }

![final result for the above code](https://miro.medium.com/max/828/1*Kd52H-jKv6N1Cwgnaz4tOA.webp)

As we can see, each ChildComponent renders now its own prop data. So this is how we can use Props for passing data and converting static components into dynamic ones.

## And we done! for the full source, read [What is Props and How to Use it in React][2]

[1]: <https://www.tutorialspoint.com/software_architecture_design/component_based_architecture.htm>
[2]: <https://itnext.io/what-is-props-and-how-to-use-it-in-react-da307f500da0#:~:text=%E2%80%9CProps%E2%80%9D%20is%20a%20special%20keyword,way%20from%20parent%20to%20child>