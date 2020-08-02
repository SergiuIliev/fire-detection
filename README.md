# README
**Project:**
Satellite Based Fire Detection Through Machine Learning

**Code Demo Video:** [Data Focused Python Final Project - Fire Watch Demo](https://www.youtube.com/watch?v=4N_lyimXBEs)

**Capabilities:**
Visualise all the fires in the target region of the word using data from historical NASA satellites and mark the most impactful fires determined by our risk algorithm.

**Installation instructions**

0. Install Python version 3.7x
1. Download _B3\_Group1.zip from Canvas or_ [_Git Repository_](https://github.com/ssaunderss/fire-detection) in the desired install directory (this will place all .py files there)
2. Download data from the following (500 mb download taking about 30s) from the following URL: 
[https://mega.nz/#!CV9VmATY!j4qQZ2f\_65dg-Oe3HZm78lk5HvYXRAdghIG5nLw4A2o](https://mega.nz/#!CV9VmATY!j4qQZ2f_65dg-Oe3HZm78lk5HvYXRAdghIG5nLw4A2o)
3. Unzip the data in the install directory / data (this will create a ./data directory with all raw and pre-processed data)
3. Install required packages (using conda or pip):
$ conda install -c plotly plotly=4.5.0
$ conda install -c conda-forge tqdm
4. Run _main.py_

**Running the program**

0. Once the installation instructions are complete and _main.py_ is being run, you will face see a pop up in your interactive python environment (screenshot attached below)

![](1.png)

1. At the popup, there are two choices you can make, either use the pre-cleaned data attached or clean fresh data to demonstrate the capability of the code. We recommend just choosing &quot;y&quot; and using the pre-cleaned data to show the end product of this project. If you choose &quot;y&quot; skip ahead to step 4

2. If you choose the &quot;n&quot; option, be prepared to buckle up for about 2 hours of data processing. The code first calls the process\_data.py file which takes in the raw satellite data and processes it so it can be fed into our risk algorithm, and eventually our heatmap visualization. When called, you can expect output similar to below, which tracks progress for this part of the data processing:

![](RackMultipart20200802-4-12dpst0_html_6bf646f58e78cd56.png)

3. Now that the data is processed and saved as a .csv, it gets passed to Risk\_Calculation.py to extract the value from the data and further distill it into the riskcalculation.csv for downstream visualization. While running the code, you can expect output similar to below, with real time tracking bars to show you the progress:

![](RackMultipart20200802-4-12dpst0_html_9180811772210491.png)

4. After choosing &quot;y,&quot; two maps will open up using localhost in your default browser (we recommend using chrome as your main browser). The first map shows the visualization of our processed satellite fire data which was run through our risk calculation algorithm. This shows the **current** risk for fires across Australia. The pop up should look like the screenshot below:

![](RackMultipart20200802-4-12dpst0_html_8dab8e65f2b3df48.png)

In another window, the second map will open which shows the historical fire information for major cities across Australia:

![](RackMultipart20200802-4-12dpst0_html_4de0d0bdfc27ca66.png)

**Code functionality**

**main.py**

- By default, it generates an analysis based on previously pre-processed data
- Switching the parameter user\_input = True main.py will re-process and combine the raw data (this operation is not multi-thread optimised yet and thus it will take approximately 2 hours on a capable computer)
- The process involves:
  - The generation of a grid over the lat/lon sector corresponding to Australia
  - Checking for each grid cell whether a fire was detected by VIIRS and/or MODIS and recording fire brightness, time between fires and detection confidence
- Calling the risk\_calculation, web scraping and visualisation functions
- Exports a CSV with the analysis results

**risk\_calculation.py**

- Calculates the risk given an input grid with brightness, confidence and time values as:
  - risk = average brightness \* average confidence / time range between fires

**visualisation.py**

- Generates an interactive map of Australia overlaying the calculated risk heatmap with the option to save the images as PNG
- NB: Depending on the data size it might take several minutes to render the map

![](RackMultipart20200802-4-12dpst0_html_8dab8e65f2b3df48.png)

![](RackMultipart20200802-4-12dpst0_html_a80cbe9bbc7f566e.png)

**Websource.py**

- Scrapes two websites: 1. A wikipedia page with a list of the historical fires in Australia, and 2. A website containing latitude and longitude information for all major cities in Australia
- Combines these two webpages to create a visualization of where historical fires have occurred in Australia
- Area burned in acres

![](RackMultipart20200802-4-12dpst0_html_4de0d0bdfc27ca66.png)

**risk\_forecast\_ML.ipynb**

- Fits a RandomForest model to our cleaned data to try and predict fire risk and fire spread

MIT License, Copyright (c) 2020, Sergiu Iliev, Austin Saunders, Peng Zeng, Yuan Li
