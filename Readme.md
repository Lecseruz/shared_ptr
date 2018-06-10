[![Build Status](https://travis-ci.org/magomedgadjiev/shared_ptr.svg?branch=master)](https://travis-ci.org/magomedgadjiev/shared_ptr)

#Shared_ptr
Manages the storage of a pointer, providing a limited garbage-collection facility, possibly sharing that management with other objects.

Objects of shared_ptr types have the ability of taking ownership of a pointer and share that ownership: once they take ownership, the group of owners of a pointer become responsible for its deletion when the last one of them releases that ownership.

shared_ptr objects release ownership on the object they co-own as soon as they themselves are destroyed, or as soon as their value changes either by an assignment operation or by an explicit call to shared_ptr::reset. Once all shared_ptr objects that share ownership over a pointer have released this ownership, the managed object is deleted (normally by calling ::delete, but a different deleter may be specified on construction).

shared_ptr objects can only share ownership by copying their value: If two shared_ptr are constructed (or made) from the same (non-shared_ptr) pointer, they will both be owning the pointer without sharing it, causing potential access problems when one of them releases it (deleting its managed object) and leaving the other pointing to an invalid location.

Additionally, shared_ptr objects can share ownership over a pointer while at the same time pointing to another object. This ability is known as aliasing (see constructors), and is commonly used to point to member objects while owning the object they belong to. Because of this, a shared_ptr may relate to two pointers:

A stored pointer, which is the pointer it is said to point to, and the one it dereferences with operator*.
An owned pointer (possibly shared), which is the pointer the ownership group is in charge of deleting at some point, and for which it counts as a use.

Generally, the stored pointer and the owned pointer refer to the same object, but alias shared_ptr objects (those constructed with the alias constructor and their copies) may refer to different objects.

A shared_ptr that does not own any pointer is called an empty shared_ptr. A shared_ptr that points to no object is called a null shared_ptr and shall not be dereferenced. Notice though that an empty shared_ptr is not necessarily a null shared_ptr, and a null shared_ptr is not necessarily an empty shared_ptr.

shared_ptr objects replicate a limited pointer functionality by providing access to the object they point to through operators * and ->. For safety reasons, they do not support pointer arithmetics.

A related class, weak_ptr, is able to share pointers with shared_ptr objects without owning them.
