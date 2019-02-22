# ETL_Project
My purpose in this project was to test the urban legend that more babies are born during a full moon thn other times of the month.


Data was obtained from the following links:

https://github.com/fivethirtyeight/data/blob/master/births/US_births_2000-2014_SSA.csv

https://www.calendar-12.com/moon_phases/2000

In the first link, the data was downloaded as a csv file to my computer. In the second case, data was scraped from the website using the Pandas read_html funtion, and looped through the years 2000 through 2014, scraping the tables from each page. 

THe csv file contains data on the number of births in the United States on every date from January 1st 2000 through December 31st of 2014.The data had to be cleaned to convert the months from numeric (1 for January eg.) to the name of the month. The month, date, and year columns had to be converted into one colums in the form used in the final database (January 1 2000, for example). This was particularly important in that the cleaned date column was used to join the two databases. Irrelevant columns were disregarded. 

The HTML file scraped and, within the loop scraping the data, cleaned and added to a list. First, the correct table had to be selected. Then that table's correct index had to be selected as it had a multi index. Any NaN values were dropped. Then the column containing the relec=vant data, the dates in a given year that were full moons, was selected. Looping through one row at a time, the value was assigned to a variable. That variable was then split at the comma, as in this example: Jan. 20, Th 11:41 PM. The first section was then added to a second vaiable to eliminate the unneccessary day of the week and time. Many of the month names were abbreviated. So the variable was put throught a series of "if elif" statements to identify if the month was an abbreviation by seeing if the first 4 letters of the string matched the abbreviated months. If so, they were repelaced with the full name of the month using the "replace" method. Once the month is corrected, if needed, the year is added, thus completing the "January 20 2000" format. This is done by using the year variable used to scrape that year's web page using the f-method. Now that the date is complete, it is appended to a list to be used to convert into a dataframe. A second list is made with the same length of the list containing all the dates of full moons saying "Full Moon". THis will be useful in the merged dataframe. THe two lists are converted into a dataframe.

THe two dataframes are joined using a left join on the "Date" column. At this point, all the dates that were full moons say "Full Moon" in the "Moon" column. ALl other rows in that column have a NaN value. THis is corrected first by filling the NaN with a space " ". I then itteratted through the rows in the "Moon" column, adding strings to a list. It occured to me now tht the "Moon" column should say simply "Full" of "Not Full." If the row contained the string "Full Moon" I added the string "FUll to the list, and if not "Not Full" was added. THen the "Moon" column was updated to the values of this list. THe dataframe was then exported to a csv file to be read in Excel. 
