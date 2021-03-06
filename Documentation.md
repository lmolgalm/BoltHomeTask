# Documentation:

The model predicts the total number of ride_values in the hexagones in Tallinn. 
It predicts a value per hour in H3 hexagons with size 6.

The model is gradient boosting over trees, implemented in the XGBoost algorithm. 
The latest version is stored in file `baseline.model`. The text representation of boosting is stored in the file `baseline_dump.txt`.

**Input**: a DMatrix table with columns

    1. h6_lat : latitude of center hexagon (Float)
    2. h6_lon : longitude of center hexagon (Float)
    3. weekdaygroups : (Uint) groups :
                                0 : Mon-Thu
                                1: Fri
                                2: Sat
                                3: sun
                                
    4. sin_seconds_zone : np.sin(2 * np.pi / 86400 * [seconds from start of day]) (Float)
    5. cos_seconds_zone : np.cos(2 * np.pi / 86400 * [seconds from start of day]) (Float)
    6. ride_value_prev_1hours : sum(ride value) for current hexagon in previous 1 hour (Float)
    7. ride_value_prev_1days : sum(ride value) for current hexagon in previous 1 day in the same hour (Float)
    8. ride_value_prev_1weeks : sum(ride value) for current hexagon in previous 1 week in the same hour (Float)
    9. dist_to_center : center of current hexagon to center of Tallin

**Output**: 
    sum(ride_value) for each inpurt row