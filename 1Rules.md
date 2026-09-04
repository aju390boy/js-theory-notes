**GIT markdown** 
> [!NOTE]
> This is an important note.

> [!WARNING]
> Be careful with this command.

> [!TIP]
> This is a useful tip.

> [!IMPORTANT]
> Remember this concept.


## Class & Interface
* You cannot use let, const, or var to declare properties inside a class or members inside an interface.
* We can use let, const, and var inside a class method because they are local variables of the method, not class properties.
* An interface only defines the structure/type of an object and does not contain implementation, so we cannot use let, const, or var inside it.

## JavaScript’s prototype-based runtime
* At runtime, JavaScript uses objects and prototype chains for inheritance and method lookup, even when we write modern class syntax.
* JavaScript has a prototype-based runtime where objects inherit properties and methods through a prototype chain; JavaScript class syntax is built on top of this prototype mechanism.

## this keyword

```ts
class User {
    name: string;

    greet(): void {
        console.log("Hello");
    }
}
```