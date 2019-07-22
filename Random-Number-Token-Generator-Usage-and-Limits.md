Random number can be generated in a step using the placeholder `${RANDOM.NUMBER}`

## Random number
**Usage:** `${RANDOM.NUMBER}` will be replaced with the current milli second. 

**Limits:** Multiple occurences of the `${RANDOM.NUMBER}` in the same step will be replaced with the same value.

## Random number of specific length
**Usage:** `${RANDOM.NUMBER:length}` will be replaced with the random number of specified length. 

`length` should be a number between 1-18

**Limits:** Every occurences of the `${RANDOM.NUMBER:length}` will be replced with a unique value.


