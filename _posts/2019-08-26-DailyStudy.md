---
layout: post
title:  "DailyStudy"
categories : DailyStudy!
date:   2019-08-26



---



## August.26~27.2019  (MON)



### Learned Today 

### 정적 메서드

```javascript
class Car {
    static getNextVin() {
		return Car.nextVin++;
    }
    constructor(make, model) {
        this.make = make;
        this.model = model;
        this.vin = Car.getNextVin();
    }
    static areSimilar(car1, car2){
        return car1.make === car2.make && car1.model===car2.model;
    }
    static areSame(car1, car2){
        return car1.vin === car2.vin;
    }
}
Car.nextVin = 0;

const car1 = new Car("Tesla", "S");
const car2 = new Car("Hyundai", "3");
const car3 = new Car("Hyundai", "3");

car1.vin; // 0
car2.vin; // 1
car2.vin; // 2

Car.areSimilar(car1, car2); // false
Car.areSimilar(car2, car3); // true
Car.areSame(car2, car3); // false
Car.areSame(car2, car2); // true
```



# **Todo List**

# **Term**

