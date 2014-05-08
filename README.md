This is a small challenge to learn more about how blocks work in Ruby. Blocks are actually very similiar to methods.

So let's think about methods for a second... You call a method with data from the outside world — the method's arguments. The code inside the method can see and use this data.

If arguments are how we pass in data into methods, blocks are how we pass in behavior. Think of them as a chunk of logic or a "brain" that your method can run (aka: "call" or "yield").

In Ruby, blocks can be passed into methods as a sort of "invisible argument", like this:

    def print_result
      result_from_block = yield
      puts result_from_block
    end
    
    # This will print out the number 9 to the console
    print_result { 3 * 3 }
    
    # Blocks can also be written using the do...end format
    print_result do
      creature = "walrus"
      "I am the #{creature}!"
    end
    
    # Very cool: blocks have access to variables outside of their definition!
    
    shopping_list = [:milk, :eggs, :cheese]
    print_result do
      important_item = shopping_list.sample # select one at random
      "I hope I don't forget #{important_item}!!!"
    end

As you will notice, the call to `yield` in the method definition is where the block is executed.

Let's write something practical using blocks. A common scenario is wanting to benchmark some code. The "skeleton" involved in benchmarking doesn't need to know what it's benchmarking, but it should be responsible for keeping track of how long it's running and other benchmarking-specific concerns.

That is, it shouldn't care whether we're benchmarking a simple function to add two numbers or something much more complicated.

Without blocks we might write code like this:
    
    start_time = Time.now
    
    # Calculate the 100th Fibonacci number
    fibonacci(100)
    
    end_time = Time.now
    
    # This will return the difference in the timestamps in seconds
    running_time = end_time - start_time
    
    puts "fibonacci(100) took #{running_time} seconds."
