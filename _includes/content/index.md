Getting Started With Signet
===========================

## What is Signet?

Signet is a fast, expressive documentation and type language for your Javascript source. Signet is not your 
parents' type system; it is rich, powerful, extensible and supports typed thinking in a way that frees you
rather than constraining you to the weakened notion of a class-based type system.

Just like Javascript, Signet treats everything as a first-class type entity including functions, objects,
arrays, numbers and others. You read correctly, Signet supports the array type out of the box, along
with refined types like int, formatted string, tuple, variant and more!

Algebraic types? Yeah, we have algebraic types. Signet supports sum types as "variant" and product types as
"tuple." Signet supports higher-kinded types as well and allows you to extend, add, mix and match your own types
any way you see fit. This means you can be as specific or generic as you like without sacrificing expression or 
the stability of your code.

Signet is a FAST run-time type checker. Instead of waiting for your code to either behave badly or throw some oddball
error, Signet will actually verify arguments against your function contract in real time and provide immediate 
feedback with meaninful messages, all in just a couple microseconds. This means you get an extra helping hand in
debugging your code without sacrificing speed or quality. You can even guard against things like argument ordering
issues with dependent type declarations.