$hidden=true 

What your CS degree (probably) didn’t teach you about code quality.  Ok, while there are many topics that could fall under this title (some of which are perhaps more important relating to soft skill) I’m going to focus on something that I find is so pervasive in CS that it’s hard to ignore. That’s Object Oriented Programming. OOP is pervasively taught in colleges all around the globe as the “right” way to program. Speaking from my own college experience we where first taught about procedural programming then we where quickly informed that this was the old way of doing things. And we where shown how OO and it’s 3 core ideas:



1. Encapsulation
1. Inheritance
1. Polymorphism 

Alongside of these values we were taught about different principles that made code “good”. 

- Loose Coupling
- Tight Cohesion
- Modularity

First off I think the thing you need to realize is that Nobody Agrees on What OO is. It’s very clear after much discussion with other people at all that peoples ideas varies wildly. As such it becomes quite difficult to make any argument any argument against it. 

The main benefits people seem to love and claim (in order of popularity): 

- OO helps you model the domain
- OO helps you write more reusable code
- OO makes more maintainable code

However, in my experience OO falls short of all of these. I’ll argue each one in turn.

OOP doesn’t help you model the domain (because you shouldn’t) One of the first things we learn in OOP is Inheritance. We learn the difference between “Is a” (a duck is an Animal) and “has a” (a duck has wings). The problem is that inheritance is the ultimate form of tight coupling. A child class is saying, “I am determined by my ancestors.” However it starts to get hairy when the children need to, you know “break the mold.” In this case we have two options: disowning the child or rewriting history to make his actions more acceptable (hoping we come up with a way to make it sound consistent) In many ways this is like a impressive fishing story that consistently gets less consistent as we modify it over time to try to fit it to our new level of impressiveness we wish to exude. 

The main problem here is that class hierarchy is rigid and exact. It makes the poor assumption that either: we are planning everything out ahead of time (waterfall style) and things won’t change, this is obviously false, even for waterfall projects. Or it makes the poor assumption that refactoring these class hierarchies will be simple or easy fixes. This is also false because it all of our code inside these classes were built with strong assumptions that those member methods and fields inherited from their parents would be there. So the only thing you have to change is everything. Not only that but all the code that deals with the child objects are calling these methods parent methods as well. 

Object hierarchies can’t represent cross cutting concerns either, meaning means common behavior that is common among lots of things that aren’t really all that related. (to give a poor ad-hoc explanation) 

The other main issue is that when you make any sort of Class you have to play this game of what is it really? Let’s try to define a common household item such as a chair. Shouldn’t be that bad right? What is a chair, really? Lets try to define a simple Class:

    class Chair inherits from Furniture implements Sittable {

      Array Legs;

      Back back;

      Seat seat;

      sit(Sitter s) {

      }

    }

Right off we see that it’s a bit weird that the a chair has a `sit` method after all it’s more of a thing to be acted upon rather than something to act. However we have all sorts of inanimate things doing things like numbers and strings in OO “doing” things so it’s not out of the norm. 

We are forced to ask questions like, “What really makes something a chair and what not?” is a table a chair? you can sit on it and it’s furniture, not to mention it has legs. For almost all intensive purposes it seems to be the exact same. What if we need to handle that case that someone would be able to do that (think a game). Where does that fit into the “Is-a” and “Has-a” relationships? 

Complicate this further here’s another example of a “Chair”. 










You can’t “sit” on it in a traditional sense but it sure looks like one, it has arm rests and a back after all which are very important parts of a chair. Perhaps it could be identified as a “Ab exercise” due to the amount of abs necessary to have a normal conversation with someone at the dinner table while “sitting” in it. 










has all the right pieces right?A broken chair is much the same as well (think errors or incomplete data). Are these considered a real chair? After all you can’t “sit” on it without bad consequences however you might be able to use it for something else you would normally use other chairs for like decoration or firewood (although not all chairs are wood). Naturally we could go the Exception route and just blow up the the make believe world ever time we encounter something unexpected or “exceptional”. 

This is modeling the absence of a field which is traditionally very hard to do with inheritance because you can’t really “uninherit” things. Sure you could make it Null but then you have all those issues of constant checking for Null. Perhaps a better example would be a stool which doesn’t have a backrest and never should. 

I find at least for myself I find this a huge waste of time. Data will be data. It’s going to be incomplete, it’s going to break the rules. Reality is alway more complex than you originally thought. Program in such a way that your entire codebase doesn’t have to change as your data gets a little more inconsistent. 

What FP buys you (and what it doesn’t)
