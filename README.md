# Election-Analysis
Performing an audit on election data using Python 

## Overview
The Purpose of this audit is to confirm congressional election results and create a detailed report of key metrics from the voting data. Additional analysis is performed to provide insight into voter turnout by county. 

## Election-Audit Results

The following outcomes were determined through this analysis: 

### - Total number of votes cast in this election:
   - **369,711**
   - Value returned using a loop, as each row in the data represents a unique vote:
        
         for row in reader:
            
            # Add to the total vote count
            total_votes = total_votes + 1
        
            # Get the candidate name from each row.
            candidate_name = row[2]

            # Extract the county name from each row.
            county_name = row[1]

### - Number and percentage of votes by county:
   - **Jefferson   10.5%   38,855**
   - **Denver      82.8%   306,055**
   - **Arapahoe    6.7%    24,801**
  
   - Values returned with a loops to get the county associated with each vote and to caluculate the percentages:
   - similar method used to find the [candidate vote counts and percentages](https://github.com/TheodoraNell/Election-Analysis/blob/main/README.md#--number-and-percentage-of-votes-by-candidate)
       
         if county_name not in County_list:
        
            # Add the existing county to the list of counties.
            County_list.append(county_name)

            # Begin tracking the county's vote count.
            county_votes[county_name] = 0

            # Add a vote to that county's vote count.
            county_votes[county_name] += 1
        
        ...
        
         for county_name in county_votes:

            # Retrieve the county vote count.
            turnout_votes = county_votes.get(county_name)
            
            # Calculate the percentage of votes for the county.
            county_turnout_percentage = float(turnout_votes) / float(total_votes) * 100
        
### - County with the largest number of votes: 
   - **Denver**
   - Value returned using a loop with a conditional to compare the percentages of votes from each county and find the highest:
   - similar method used to find the [winning candidate](https://github.com/TheodoraNell/Election-Analysis/blob/main/README.md#--winning-candidate-diana-degette)

         if (turnout_votes > turnout_count) and (county_turnout_percentage > turnout_winning_percentage):
        
            turnout_count = turnout_votes
            highest_turnout = county_name
            highest_percentage = county_turnout_percentage

### - Number and percentage of votes by candidate:
   - **Charles Casper Stockham   23.0%   85,213**
   - **Diana DeGette             73.8%   272,892**
   - **Raymon Anthony Doane      3.1%    11,606**
  
   - Values returned in a similar method to getting [votes by county](https://github.com/TheodoraNell/Election-Analysis/blob/main/README.md#--number-and-percentage-of-votes-by-county)

### - Winning Candidate: 
   - **Diana DeGette**
   - **Vote Count: 272,892**
   - **Percent of Votes: 73.8%**
  
   - Values returned in a similar method to getting the county with the [largest voter turnout](https://github.com/TheodoraNell/Election-Analysis/blob/main/README.md#--county-with-the-largest-number-of-votes-denver)
      
      
## Election-Audit Summary

The script used in this analysis could be modified and used to audit future elections with the same voting system as well as refactored for use with different voting systems and to get additional metrics. Possible examples include:

- For elections where the winner is determined by the number of voting districts they win (instead of majority of overall votes) the script could be edited to first find the winning candidate for each county and then compare the number of wins for each candidate to find the winner, factoring in any possible point value differences for larger or smaller districts.

- For elections with multi-winner voting systems the script to find the winning candidate could be edidted to return multiple winners with the x number of highest ranking vote counts depending on the number of open seats. Possible considerations would be the type of multi-winner system used (block, single, or cumulative voting)

- If the data is available, getting the relative county voter turnout in addition to the overall allows for deeper analysis since counties with larger populations will most likely have higher turnouts in elections but smaller counties might have higher relative turnout. This refactoring could possibly be achieved with the addition of a dictionary of registered voters (or eligible voters) by county. The county votes would then be divided by the value for that county and multiplied by 100 to find the relative percentage. 
