## Running the Program

11/17/2025 

So, I got the code running.

First full run was with the following json parameters:

### Working JSON - copied from Zenodo with custom infill
```json
{
    "material": "magnetite",
    "sizes": {
        "list": [
            {
                "value": 30,
                "fraction": 1.0
            }
        ],
        "unit": "nm"
    },
    "elongations": {
        "list": [
            {
                "value": 30,
                "fraction": 1.0
            }
        ]
    },
    "directions": {
        "list": [
            {
                "value": [
                    1.0,
                    0.0,
                    0.0
                ],
                "fraction": 1.0
            }
        ]
    },
    "applied_field": {
        "strength": 30,
        "direction": [
            1,
            0,
            0
        ],
        "unit": "uT"
    },
    "cooling_regime": {
        "ambient_temperature": 15.0,
        "initial_temperature": 579.9999,
        "reference_time": 6E1,
        "temperature_at_reference_time": 15.15,
        "allowable_percentage_drop": 0.005,
        "stopping_temperature": 50
    },
    "outputs": {
        "model": "model.csv"
    },
    "tau0": 1e-10,
    "epsilon": 1e-14,
    "n_polish": 0
}
```
I used a `size` of 30, an `elongation` of 30, `applied_field` of 30 with `direction` [1, 0, 0]. and `reference_time` of 6E1, as one can see. Those were the parameters that were left open in the Zenodo file. The main issue, as far as I could tell from the debug messages, was that the `epsilon` parameter in the `.json` file simply cannot be 1E-15. The program crashed each time I tried that. It was only after decreasing that parameter that the program started running. As you can see, I put `n_polish` equal to 5. It seems to be doing another run fine with that set to 0.

This takes a while to run, but the way I was able to track this was with the debug output of `temperature`, it helped sanity check me that the program was going somewhere.

The `allowable_percentag` parameter does help control that temperature stepping.

Now that I had a working JSON file, I decided to check out the RELEASE version I had compiled earlier. It runs, and runs quite a bit more quickly than the DEBUG version. Probably not a suprise to folks who are smarter than me, but it was quite a difference.
