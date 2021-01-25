# Lambda Expression
* Purpose
     
     Deferred Excution (load when need)
* Rules

    1. Can't mutate captured variable
    2. Can't capture variables that changes outside the block (varibles need to be effectively final)
    3. Can't declear variables that have same name with the local varibles
    4. "this" points to the creater method's this
    
* Advantages

    1. Reducing objects created (autoboxing, anunymous classes)
