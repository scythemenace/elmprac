
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

```type State``` has to be added to something that is also a state data type (called Model - written as ```type alias Model```)
Regards to animation slot, only thing that is in the ``` type alias Model ``` is time (we use ```model.time```)

It looks like this

```
type alias State
    {
        time: Float,
        state: State
    }

```

```state: State``` means we are just using that datatype to keep track of states being changed.

Then there is a function called ```view``` that takes in the model and displays it.

The code is somewhat like this:-

```
view model = collage 192 128 (myShapes model)

```
In the above code the function ```collage``` converts our Shapes into SVG and embed that into HTML in order to view them.
We are converting ```myShapes model``` into an SVG which has a dimension of 192 x 128.

Here is a sample code for myShapes model:-

```
myShapes model model =
    case model.state of 
        Welcome -> 
            [ text "Welcome"
                |> centered
                |> filled black
            , group
                [ roundedRect 40 25 5 
                    |> filled green
                , text "Transition 3"
                    |> centered
                    |> size 8
                    |> filled black
                    |> move (0, -3)

                ]
                    |> move (0, -25)
                    |> notifyTap Transition1
            
            ]
        State2 -> 
            [ text "State 2"
                |> centered
                |> filled black
            , group
                [ roundedRect 40 25 5 
                    |> filled green
                , text "Transition 4"
                    |> centered
                    |> size 8
                    |> filled black
                    |> move (0, -3)

                ]
                    |> move (0, -25)
                    |> notifyTap Transition2 
            
            ]

```
What is happening in the above code, is that the roundedRect and the text form a button, and the notifyTap function checks for user input i.e. if the user clicks on that button and returns an output.

Then we have the update
```
update msg model = 
    case msg of 
        Tick t ->
            { model | time = t }
        Transition3 ->
            case model.state of
                Welcome ->
                    { model | state = State2 }
                otherwise ->
                    model
        Transition4 ->
            case model.state of 
                State2 ->
                    { model | state = Welcome }
            otherwise ->
                model
```

In the above code, our case expression matches the messages i.e. the inputs we are getting from the app. The ```Tick``` message checks if an animation is going on and makes sure they have the correct time, so the animation is moving properly.

If we get ```Transition3``` then we run another ```case``` which checks if our state is Welcome. If it is then it transitions it to the mentioned state which is ```State2``` in this case, otherwise, it will just lead to model.

If we get ```Transition4``` then we run another ```case``` which checks if our state is State2. If it is then it transitions it to the mentioned state which is ```Welcome``` in this case, otherwise it will just lead to model.

