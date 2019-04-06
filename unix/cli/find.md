# find

Iterate over files safely:

`find . -type f -print0 | xargs -0 -n1 echo`
