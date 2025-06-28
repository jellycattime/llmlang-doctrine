# LLMLang Examples

---

## Variables and Assignment

```plaintext
set_var name str "Alice"
set_var age int 30
add_int age 5 to age_plus_five
````

---

## Mathematical Operations
```plaintext
set_var a int 10
set_var b int 7

add_int a b to sum
sub_int a b to diff
mul_int a b to prod
div_int a b to quot
mod_int a b to rem

print_int sum
print_int diff
print_int prod
print_int quot
print_int rem

set_var x float 2.5
set_var y float 4.0

add_float x y to fsum
sub_float y x to fdiff
mul_float x y to fprod
div_float y x to fquot

print_float fsum
print_float fdiff
print_float fprod
print_float fquot
```

---

## Type Conversion Operations

```plaintext
set_var a int 8
set_var b float 3.2

# Convert int to float
int_to_float a to a_f
add_float a_f b to sum_f
print_float sum_f  # 8.0 + 3.2 = 11.2

# Convert float to int (truncates the decimal part)
float_to_int b to b_i
add_int a b_i to sum_i
print_int sum_i    # 8 + 3 = 11

# Example: convert string to int
set_var s str "42"
try_parse_int s to ok, num
if ok
    add_int num 1 to res
    print_int res
else
    print_str "Error"
end_if

# Example: convert int to string
set_var n int 123
int_to_str n to n_str
concat_str "Value: " n_str to out
print_str out
```

---

## String Concatenation and Variable Insertion

```plaintext
set_var name str "Alice"
set_var city str "Paris"

# Concatenation of strings
concat_str "Hello, " name "! Welcome to " city "." to greeting
print_str greeting  # Output: Hello, Alice! Welcome to Paris.

# Inserting variables into strings using $
set_var user str "Bob"
set_var item str "apple"
set_var quantity int 3

set_var message str "User $user bought $quantity $item(s)."
print_str message  # Output: User Bob bought 3 apple(s).

# Escaping the $ symbol in strings
set_var price int 100
set_var price_str str "Price: \$$price"
print_str price_str  # Output: Price: $100

# For a literal $ character (not a variable), use \$
set_var example str "Total is \$50"
print_str example  # Output: Total is $50
```

---

## Functions

```plaintext
function greet person_name str -> msg str
    concat_str "Hello, " person_name "!" to msg
end_function

call greet name to message
print_str message
```

---

## Structs

```plaintext
struct Person
    field name str
    field age int
end_struct

set_var p Person
set_field p name "Ivan"
set_field p age 33

get_field p name to person_name
print_str person_name
```

---

## Methods

```plaintext
function say_hello self Person
    get_field self name to n
    concat_str "Hi, " n "!" to msg
    print_str msg
end_function

call say_hello p
```

---

## Arrays

```plaintext
array users str dynamic
array_push users "alice"
array_push users "bob"
array_push users "charlie"

call join users ", " to result
print_str result
```

---

## Map/Dictionary

```plaintext
map phonebook str int
map_set phonebook "Alice" 12345
map_get phonebook "Alice" to phone
print_int phone
```

---

## Control Flow

```plaintext
set_var a int 10
if a > 5
    print_str "Greater than 5"
else
    print_str "Less or equal to 5"
end_if
```

---

## Loops

```plaintext
# While-like loop
set_var i int 0
loop while i < 3
    print_int i
    add_int i 1 to i
end_loop

# Foreach over array
array fruits str dynamic
array_push fruits "apple"
array_push fruits "banana"
array_push fruits "cherry"

foreach fruit in fruits
    print_str fruit
end_foreach

# Loop over range
loop for j from 1 to 5
    print_int j
end_loop
```

---

## Pipeline Chaining

```plaintext
set_var src str "  test-value-123  "
call trim src -> replace "-" "_" -> upper to result
print_str result
```

---

## Error Handling

```plaintext
set_var s str "42x"
try_parse_int s to ok, n

if ok
    add_int n 1 to next
    print_int next
else
    print_str "Not a number"
end_if
```

---

## Try-Catch Error Handling
```plaintext
try
    set_var input str "abc"
    try_parse_int input to ok, num
    if ok
        add_int num 10 to out
        print_int out
    else
        throw "Not an integer"
    end_if
catch err
    print_str "Error: "
    print_str err
end_try
```

---

## Working With Struct Arrays

```plaintext
struct User
    field name str
    field age int
end_struct

array users User dynamic

set_var u1 User
set_field u1 name "Ivan"
set_field u1 age 30
array_push users u1

set_var u2 User
set_field u2 name "Olga"
set_field u2 age 28
array_push users u2

call map users get_field age to ages
call join ages ", " to out
print_str out
```

---

## Multithreading

```plaintext
function worker id int
    concat_str "Thread " id " working" to msg
    print_str msg
end_function

set_var t1 thread
set_var t2 thread

thread_start t1 worker 1
thread_start t2 worker 2

thread_join t1
thread_join t2
```

---

### Async Tasks (Green Threads)
```plaintext
function async_job value int
    print_str "Job started"
    sleep 1
    add_int value 10 to result
    print_str result
end_function

set_var task1 async
set_var task2 async

async_start task1 async_job 5
async_start task2 async_job 7

async_wait task1
async_wait task2
```

---

⚠️ **Warning:**  
In LLMLang, always use `call` for method or function invocation instead of dot notation (`object.method()`).  
This ensures maximal clarity and removes ambiguity for both humans and LLMs.

Example:  
```plaintext
call process_user p x y
````
Here, p is explicitly passed as the first argument to the function, representing the target object or structure instance—there is no implicit "self" or hidden receiver. All parameters are always listed in order as defined in the function signature.

**Not:**

```plaintext
p.process_user(x, y)
```

Chaining (pipeline with `->`) may be used for linear transformations to save tokens and context.
However, stepwise `call ... to ...` is always preferred for clarity, debugging, and maximum LLM interpretability.
Use chaining **only** if the context window is tight or token savings are essential.

**Preferred:**

```plaintext
call trim s pattern flag to s1
call upper s1 locale option to s2
call concat_str prefix s2 suffix to out
```

**Chaining (only if needed):**

```plaintext
call trim s pattern flag -> upper locale option -> concat_str prefix _ suffix to out
```
