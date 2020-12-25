---
title: A Generic Design of linked list in C
date: 2020-12-25 18:35:57
tags:
---

<div style="text-align: left">

Linked list is a very important data structure. In `C++`, with the support of templating, we can implement a template linked likst class and use it for any data type we want. However, in `C`, there is no such thing like templating. How can we implement a generic linked list? It is tedious to re-implement functions like `list_add` and `list_remove` for every data type that needs to be linked. Besides, it is hard to make one node in two lists simultaneously.

A traditional linked list node is something like this:
```c
typedef sturct NodeA nodea_t;
struct TraditionalNode {
    nodea_t *prev;
    nodea_t *next;

    // fields
    int val1;
    char val2;
    // maybe more fields
};
```
With this design, one needs to implement a set of functions for every type of traditional node. This type of node is like a link-able node with extra data fields. 

---
The design of generic linked list takes the pointers (linkable part) out of the data node. It enables more possible uses. The design is:
```c
typedef struct ListNode list_node_t;
struct ListNode {
    list_node_t *prev;
    list_node_t *next;
};

typedef struct List {
    // dummy nodes
    list_node_t head;
    list_node_t tail;
} list_t

typedef struct NodeB {
    list_node_t tag_in_list_a;
    list_node_t tag_in_list_b;
    // fields
    int val1;
    char val2;
    // maybe more fields
} nodeb_t;
```

This design defines a linkable type `list_node_t` and a list type `list_t`, and put one or more members of `list_node_t` type in the actual data structure that needs to be linked. We only need to implement functions for `list_t` and `list_node_t`, then we are done.

A possible implementation of `list_push_back` could be like this:
```c
void list_push_back(list_t *l, list_node_t *node) {
    list_node_t *last = l->tail.prev;
    last->next = node;
    node->prev = last;
    node->next = &(l->tail);
    l->tail.prev = node;
}
```

To use `list_push_back` for `nodeb_t`, we will use some macros:
```c
// uintptr_t is a type for address.

#define __member_offset(struct_type, member) \
    (uintptr_t)(&((struct_type*)0)->member)

#define __container_of(struct_type, member, node_ptr) \
    (struct_type*)( \
        (uintptr_t)node_ptr - __member_offset(struct_type, member) \
    )
```
`__member_offset` is a macro calculates the offset of `member` in `struct_type`. For example, the offset of `tag_in_list_a` in `nodeb_t` is `0` and that of `tag_in_list_b` is `sizeof(list_node_t)`.

`__container_of` is to find the pointer to `struct_type` by a pointer `node_ptr` to `member`.

With this two macros, we can define the follow macro:

```c
#define __list_push_back(list, container_ptr, member) { \
    list_node_t *p = &(container_ptr->member); \
    list_push_back(list, p); \
}
```
Sample usage:
```c
list_t *list_a;
list_t *list_b;

nodeb_t *nb;

// push nb into list_a
__list_push_back(list_a, nb, tag_in_list_b);
// push nb into list_b
__list_push_back(list_a, nb, tag_in_list_b);
```

---
As we can see, this generic design is easy to use and solve the problem for push one node into different lists simultaneously.

</div>