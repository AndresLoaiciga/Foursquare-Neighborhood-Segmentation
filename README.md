# Foursquare-Neighborhood-Segmentation

Comparing Neighborhoods in The Bronx and Brooklyn using _k_-means Clustering
-----------------------------------------------------------------
__Introduction:__ Brooklyn is on the rise while The Bronx is unfortunately in decline. I myself am a native New Yorker and grew up and spent most of my life in The Bronx. I very much like my neighborhood, but it's a long commute to lower Manhattan and it has an older median age. I have been thinking about relocating to Brooklyn to be closer to lower Manhattan and to be around more people my age. In this project I want to segment the different neighborhoods in both The Bronx and Brooklyn to see which, if any, neighborhoods in Brooklyn are closely related to my neighborhood in The Bronx. I am going to use the Foursquare API to compare the neighborhoods based on the venues (restaurants, bars, gyms, etc...) present in the different neighborhoods.

__Getting the Data:__ In order to create the data frame I needed to first download a json file. This json contains all the names, the borough, and latitude and longitude of every neighborhood in New York City. The code below is how I extracted the json file from the internet: 

![image](https://user-images.githubusercontent.com/35437820/56395484-ce2fa480-6208-11e9-919c-a19c5e003d8c.png)

All of the relevant data I needed was in the features key. So I defined a new variable that included the features data . Below is what the data looked like before I transformed the data into a _Pandas_ dataframe:

![image](https://user-images.githubusercontent.com/35437820/56395606-3ed6c100-6209-11e9-9b23-87b66d425784.png)

The feature key contains the four items I need for my dataframe (Borough, Neighborhood, Latitude and Longitude). Next I created a blank Pandas data frame, and then looped the json data into the new _Pandas_ data frame using the for loop below:

![image](https://user-images.githubusercontent.com/35437820/56395723-c15f8080-6209-11e9-9f2b-608e130e8f3b.png)

Now that my data is in a _Pandas_ dataframe, it'll be much easier to manipulate and examine. Since I am only interested in neighborhoods in The Bronx and Brooklyn, I simply dropped all the rows that contained neighborhoods in Manhattan, Queens and Staten Island. Yes, Staten Island is still technically a borough of NYC. I know it's easy to forget about. Next I needed to get the top 100 venues within a 750 meter radius of each neighborhood using the Foursquare location API. I used the code below to do that:

![image](https://user-images.githubusercontent.com/35437820/56395857-4e0a3e80-620a-11e9-8d9b-8b4b5025e52c.png)

From here I needed to transform the json data into a Pandas dataframe like I did above and merge the 2 dataframes together in order to have one dataframe. Now that the data frame was complete I was ready to do some exploration and further manipulation of the data.

__Exploratory Data Analysis:__ Once I had my dataframe created I was ready to explore the data. For this project I wanted to map out the neighborhoods and eventually group them into 5 different clusters. Firstly I just wanted to map out the different neighborhoods and make sure my map looked good.  So the first thing I did was plot out the neighborhoods of the Bronx and Brooklyn using the Python _Folium_ library. I used the latitude and longitude of each neighborhood and the map came out as below:

![image](https://user-images.githubusercontent.com/35437820/56395976-d4268500-620a-11e9-8969-c13d384ca5c1.png)

Everything looks good to me. From there I wanted to do the same thing, but only look at the venues that are located in my neighborhood, Pelham Bay. There were only 53 venues found in my neighborhood. The map is visualized below: 

![image](https://user-images.githubusercontent.com/35437820/56396054-28316980-620b-11e9-8dae-71ba176d40cd.png)

My neighborhood is very residential and located next to the largest park in New York City, so most of the venues are located on 2 or three streets. The first five rows of the data frame used to map it looked like this:

![image](https://user-images.githubusercontent.com/35437820/56396135-7a728a80-620b-11e9-8ec8-c9c1dd7a5a33.png)

I was ready to group all the categories of the different venues in each neighborhood in The Bronx and Brooklyn. There were 354 unique venue categories ranging everywhere from Adult Boutiques to Speakeasies to Zoos and of course Pizza Parlors. I then had to encode the data and get dummy variables of all the different categories. Once I did that I was able to break down the frequency of the different categories of each neighborhood. The 5 most frequent venues for my neighborhood are listed below:

![image](https://user-images.githubusercontent.com/35437820/56396238-e5bc5c80-620b-11e9-90e6-63c6c0274c59.png)

Now I was almost ready to start clustering the neighborhoods. To make things easier I only wanted to use the top 10 venues in each neighborhood for comparison. I created a new dataframe with the neighborhoods and the top 10 venues and the top 5 rows  which looked like this:

![image](https://user-images.githubusercontent.com/35437820/56397290-0e932080-6211-11e9-9234-330ad92764e0.png)

Once that was done I could run a _k_-means clustering algorithm on the data and assign a cluster to every neighborhood that was similar to one another. From there I was able to look at my results and compare the neighborhoods. 

__Results:__ After I ran the k-means clustering on the data and added the clusters to the data frame I wanted to map out all the different clusters to get a nice visualization of the similar neighborhoods. Below is the map with my neighborhood pointed out:

![image](https://user-images.githubusercontent.com/35437820/56397356-629e0500-6211-11e9-93b3-a70bdefca432.png)

__Conclusion:__ My neighborhood, Pelham Bay was located in the largest cluster of all of them. Apparently my neighborhood isn't to unique. My neighborhood is much more like most other Bronx neighborhoods and southern and eastern Brooklyn neighborhoods. I was thinking about moving to the north eastern part of Brooklyn (the green cluster). Apparently it's not as similar to my neighborhood as I would've thought. I'm sure it has to do with the gentrification of those Brooklyn neighborhoods and hipster influence on them. Like I stated in the introduction my neighborhood has a high median age, which would have an affect on what type of venues would be in each neighborhood. 

Some further examination to be done:
Add more clusters.
Look at features such as crime rate, demographics, and median age of each neighborhood. 
Use the top 20 or 30 venues next time instead of just the top 10. 

Thanks for reading and feel free to see all the code above. Also visit my website to see this project and other projects at www.andrewcarl.nyc 
