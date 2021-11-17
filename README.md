# surfs_up_Analysis

## Overview of surfs_up analysis

We are trying to determine the better place to create a surf store. We need some investor, but we need to analyse the weather of the region to guarantee that the store business will be successful.

### Purpose

Using pandas, sqlite and flask, we are analysing some weather date to important aspects for the store. Specially we are looking at the temperature data for June and December in Oahu, to determine if the surf and ice cream shop bussinnes is sustainable year round.

### surfs_up analysis results

For the first party of the analysis, we need to access our weather database. To do this we are using sqlite.

    # Dependencies
    import numpy as np
    import datetime as dt
    import pandas as pd

    # Python SQL toolkit and Object Relational Mapper
    import sqlalchemy
    from sqlalchemy.ext.automap import automap_base
    from sqlalchemy.orm import Session
    from sqlalchemy import create_engine, func

    engine = create_engine("sqlite:///hawaii.sqlite")

    # reflect an existing database into a new model
    Base = automap_base()
    # reflect the tables
    Base.prepare(engine, reflect=True)

    # Save references to each table
    Measurement = Base.classes.measurement
    Station = Base.classes.station

    # Create our session (link) from Python to the DB
    session = Session(engine)
    
As next step, we are looking for the temperatures for the month of June, so we can get a summary statistics.

    # 1. Import the sqlalchemy extract function.
    from sqlalchemy import extract

    # 2. Write a query that filters the Measurement table to retrieve the temperatures for the month of June. 
    results = session.query(Measurement.date, Measurement.tobs).filter(extract('month', Measurement.date)==6).all()
    print(results)
    
![image](https://user-images.githubusercontent.com/88845919/142086216-2317c1b6-6148-47c9-9916-11d6a4973c9d.png)

Then, we made the same analysis for December

    # 6. Write a query that filters the Measurement table to retrieve the temperatures for the month of December.
    results = session.query(Measurement.date, Measurement.tobs).filter(extract('month', Measurement.date)==12).all()
    print(results)
    
![image](https://user-images.githubusercontent.com/88845919/142086338-4a555d5d-bc2a-4b0c-8e08-8d6e3b3314d8.png)

With this we can notice that:
- The mean temperature for the two months has only 4° of difference, so the weather doesn´t change that much. Thats a good point.
- Other important point to consider is that the minimum temperature regist is 9° lower on December that June. This could be represent a pdroblem.
- And as last point, me maximum temperature regist for this months has only a difference of 3°. So the variation isn´t that much.
