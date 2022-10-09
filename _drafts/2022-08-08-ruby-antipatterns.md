---
title: "Ruby Antipatterns"
categories: ["ruby", "programming"]
---


```ruby
    @cars.each do |car|
      @car = car # why does this need to be instance variable?
      @miles_driven = 0 # why does this need to be instance variable?
      @drvier = car.driver # why does this need to be instance variable?
      next if @driver.nil? # this will always be true because there is typo in instance variable before
      
      drive_car() # this doesnt accept any arguments, you don't know what this method requires to execute because of "instance variable" leaking everywhere
      
      if @miles_driven == 0 # how was @miles_driven changed?
        puts "Car is broken" # this is not error logging, neither error handling, also no information to indentify what car object it was
        @cars.delete(@car) # changing enumerator while iterating over it is a bad idea
      end
    end
```