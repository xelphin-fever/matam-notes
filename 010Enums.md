## C

# Enum 

This is an Enum:
```cpp
enum Day {SUNDAY, MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY , SATURDAY, DAY_NUM};
```
SUNDAY == 0, MONDAY == 1, ... SATURDAY == 6, DAY_NUM == 7

It can keep an integer value for each element in a set of constants. 

## Usage

```cpp
enum Day today = TUESDAY;
enum Day favourite_days[FAVS] = {FRIDAY, SATURDAY};

printf("today is: %d \n", today); // today is: 2
```

## Usage with Functions

Enums can be particularly useful when used with functions. 

```cpp
enum Day whatDay (enum Day curr, int jumpDays)
{
  enum Day futureDay = (curr + jumpDays) % DAY_NUM;

  return futureDay;
}
```
We can use ```whatDay()``` to calculate the day x days from DAY.
```cpp
printf("Today is Monday == 1. In 8 days it will be day: %d \n", whatDay(MONDAY, 8));
}
```
