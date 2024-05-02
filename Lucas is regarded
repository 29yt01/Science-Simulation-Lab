import numpy as np

# Define constants
DISTANCE_FROM_HEATER = 25  # cm
MAX_HEAT_TIME = 5  # minutes
SOLAR_HEATER_EFFICIENCY = 0.8  # assumed efficiency of solar heater
GASOLINE_HEATER_EFFICIENCY = 0.5  # assumed efficiency of gasoline heater

# Define material properties
NICKEL_CONDUCTIVITY = 90.9  # W/mK (at 20°C)
COPPER_CONDUCTIVITY = 386  # W/mK (at 20°C)

# Define heater properties
SOLAR_HEATER_POWER = 100  # W (max power of solar heater)
GASOLINE_HEATER_POWER = 500  # W (max power of gasoline heater)

# Define battery properties
SOLAR_HEATER_BATTERY_CAPACITY = 200  # Wh (capacity of solar heater battery)
GASOLINE_HEATER_BATTERY_CAPACITY = 1000  # Wh (capacity of gasoline heater battery)

# Simulation function
def simulate_experiment(material, heater_type):
    # Initialize variables
    conductivity = 0
    battery_life = 0
    
    # Apply heat for 5 minutes
    if heater_type == 'solar':
        power = SOLAR_HEATER_POWER
        efficiency = SOLAR_HEATER_EFFICIENCY
        battery_capacity = SOLAR_HEATER_BATTERY_CAPACITY
    elif heater_type == 'gasoline':
        power = GASOLINE_HEATER_POWER
        efficiency = GASOLINE_HEATER_EFFICIENCY
        battery_capacity = GASOLINE_HEATER_BATTERY_CAPACITY
    
    heat_flux = power / (DISTANCE_FROM_HEATER ** 2)  # W/m^2
    temperature_increase = heat_flux * MAX_HEAT_TIME * 60  # K
    
    # Calculate conductivity based on material properties
    if material == 'nickel':
        conductivity = NICKEL_CONDUCTIVITY * (1 + 0.01 * temperature_increase)  # W/mK
    elif material == 'copper':
        conductivity = COPPER_CONDUCTIVITY * (1 + 0.005 * temperature_increase)  # W/mK
    
    # Calculate battery life
    energy_consumption = power * MAX_HEAT_TIME * 60 / 3600  # Wh
    battery_life = battery_capacity - energy_consumption
    
    return conductivity, battery_life

# Run simulation for each material and heater type
results = {}
for material in ['nickel', 'copper']:
    for heater_type in ['solar', 'gasoline']:
        conductivity, battery_life = simulate_experiment(material, heater_type)
        results[f"{material}_{heater_type}"] = {'conductivity': conductivity, 'battery_life': battery_life}

# Print results
print("Results:")
for key, value in results.items():
    print(f"{key}: Conductivity = {value['conductivity']} W/mK, Battery Life = {value['battery_life']} Wh")
