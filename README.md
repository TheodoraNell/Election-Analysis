# Election-Analysis
Performing an audit on election data using Python 

## Overview
The Purpose of this audit is to confirm congressional election results and create a deatailed report of key metrics from the voting data. Additonal analysis is performed to provide insight into county-specific voting trends as well as voter turnout. 

## Election-Audit Results

The following outcomes were determined through this analysis: 

### - Total number of votes cast in this election: **369,711**
   value returened using a loop, as each row in the data represents a unique vote:

        for row in reader:
            
            # Add to the total vote count
            total_votes = total_votes + 1
        
            # Get the candidate name from each row.
            candidate_name = row[2]

            # Extract the county name from each row.
            county_name = row[1]

### - Number and percentage of votes by county
      - **Jefferson   10.5%   38,855**
      - **Denver      82.8%   306,055**
      - **Arapahoe    6.7%    24,801**
  
   values returned with a loops to get the county associated with each vote and to caluculate the percentages:
   (similar method used to find the [candidate vote counts and percentages](https://github.com/TheodoraNell/Election-Analysis/blob/main/README.md#--number-and-percentage-of-votes-by-candidate)
       
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
        
### - County with the largest number of votes: **Denver**
   value returned using a loop with a conditional to compare the percentages of votes from each county and find the highest:
   (similar method used to find the [winning candidate](https://github.com/TheodoraNell/Election-Analysis/blob/main/README.md#--winning-candidate-diana-degette))

        if (turnout_votes > turnout_count) and (county_turnout_percentage > turnout_winning_percentage):
            turnout_count = turnout_votes
            highest_turnout = county_name
            highest_percentage = county_turnout_percentage

### - Number and percentage of votes by candidate
   **Charles Casper Stockham   23.0%   85,213**
   **Diana DeGette             73.8%   272,892**
   **Raymon Anthony Doane      3.1%    11,606**
  
   Values returned in a similar method to getting [votes by county](https://github.com/TheodoraNell/Election-Analysis/blob/main/README.md#--number-and-percentage-of-votes-by-county)

### - Winning Candidate: **Diana DeGette**
   **Vote Count: 272,892**
   **Percent of Votes: 73.8%**
  
   Values returned in a similar method to getting the county with the [largest voter turnout](https://github.com/TheodoraNell/Election-Analysis/blob/main/README.md#--county-with-the-largest-number-of-votes-denver)
      
      
## Election-Audit Summary

- possible uses for future elections: 
  - refactor for larger docket of candidates? 
  - Use county populations to get voter turnout percentage of each county and target voter accessability in those areas
