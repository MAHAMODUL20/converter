# converter
def convert_temperature(temperature, from_unit, to_unit):
    """Converts temperature between Celsius, Fahrenheit, and Kelvin.

    Args:
        temperature: The temperature value to convert.
        from_unit: The unit of the input temperature (e.g., "C", "F", "K").
        to_unit: The desired unit for the converted temperature.

    Returns:
        The converted temperature value.
    """

    if from_unit == to_unit:
        return temperature

    conversion_factors = {
        ("C", "F"): lambda t: (t * 9 / 5) + 32,
        ("C", "K"): lambda t: t + 273.15,
        ("F", "C"): lambda t: (t - 32) * 5 / 9,
        ("F", "K"): lambda t: ((t - 32) * 5 / 9) + 273.15,
        ("K", "C"): lambda t: t - 273.15,
        ("K", "F"): lambda t: ((t - 273.15) * 9 / 5) + 32
    }

    try:
        conversion_function = conversion_factors[(from_unit, to_unit)]
        return conversion_function(temperature)
    except KeyError:
        raise ValueError(f"Invalid units specified: {from_unit} and {to_unit}")

# Get user input
temperature = float(input("Enter the temperature: "))
from_unit = input("Enter the unit of the temperature (C, F, K): ").upper()
to_unit = input("Enter the desired unit (C, F, K): ").upper()

# Convert and print the result
converted_temperature = convert_temperature(temperature, from_unit, to_unit)
print(f"{temperature} {from_unit} is equal to {converted_temperature} {to_unit}")
