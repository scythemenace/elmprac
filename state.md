
## Importance of State diagrams in our Elm UI
Model Driven Development (MDD) is about speeding the development process. In our case the state diagrams were a way to speed up this process, otherwise we would have taken so much time to modify the cases, update function, etc. if we created everything from scratch

## How is model development engineering (EE) different from (MDD)
Model driven engineering is about simulating the device, not just generating the code i.e. being able to identify properties of the software

So basically using states is a way of overviewing what functionality our app has. Otherwise, we would have to manually test every feature that we have and then implement changes which wastes a lot of time.

## When would we want our user to be stuck in a particular state
Maybe, if we have a game, where we want a feature that if a user falls on a trapdoor, he falls into a dungeon where he cannot climb out of.

## Code part
We create two types:- In this context, we call one of the types ```State``` (we can call it anything, but in this context calling this custom data type State helps us understand what it is in context to this App) and the other data type is ```Msg```(We could have called it transitions, but we call it ```Msg``` to stick to the convention of Elm because Msg is a type used in ```View```)

It looks somewhat like this
```
type Msg = Tick Float GetKeyState
            | Transition 1
            | Transition 2

type State = Welcome
            | State 2 

-- We only have two states in this example

```

<span style="color: red;">Some</span>

```type State``` has to be added to something that is also a state data type (called Model - written as ```type alias Model```)
Regards to animation slot, only thing that is in the ``` type alias Model ``` is time