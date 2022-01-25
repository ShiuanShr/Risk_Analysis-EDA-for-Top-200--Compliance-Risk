**Preface:**

We can only share very limited demo (stored at private drive (leo.shr@iss.nthu), kindly ask for permission)  to prove the existance of the project because it contain clients personal information (trading amount, location, frequency, pattern cluster, trading cryptocurencies, etc.) and the project result belongs to company. Even though we have unlabeledized the data and replaced the privacy information with eligible ID, it still only allowed to be used for the purpose of user experience improvement or for internal AML regulartory. Last but not the least, due to the current GDPR policy in our EU clients, the automatic profiling is no longer allowed without additional consent papers, not to mentioned for data analyst's personal project.

However, as a leader of this project, we could briefly talk about how we implement the project.

In the beginning, it was EDA for risk report without the precedent case.
The raw data was extremely dirty beyond our expectations and came from the backend.
After complex data cleaning process and text mining preprocessing, we get relative 'cleaned' monthly-based trading record datasets for over 50 countries Bitfinex served.
It was a massive scale dataset. Therefore, we randomly picked one country's dataset as the first profiling target and then applied the following data process on the rest of them after we construct the mature data pipeline.

**To be brief, here are some illustrations for this month-long project:**

1. That was a massive scale dataset, hence, only data pipelines were suitable for it. As the result, the project was conducted by python. However, the visualization part was required to use GoogleSilde for presentation due to the administrative manager's requirements. Hence, in order to build the linkage between G-slides and G-spreadsheet, we have to extract the data and the plot we want via data pipeline and load only a limited size into google spreadsheet because the spreadsheets did not support the API we needed after all the data analysis works. However, for the trial demo, we use simply Excel and Google Spreadsheet directly for concept demonstration.

2. Most of the data are noises. Therefore, a certain degree of feature engineer helps. However, mostly, the important variables simply depend on what AML expertise told us.

3. It contains lots of idle accounts, which trading frequency is almost equal to 0. This kind of account increased the sparse level of data. But they can not be discarded due to the probability of the providers of dummy accounts. Moreover, the criminal account would not exist alone, mostly, they would use plenty of dummy accounts to lower the transparency of cash flow  to escape from criminal investigation. And have to say, under the property of blockchain, it would be almost unlikely to trace for outsiders (Gov AML related Competent Authority) if the investigators or risk analysts in crypto exchange are neglected of duty. Back to the topic, what we did is trying to point out 'sets' of accounts having highly suspicious trading relationships from million trading records and turn over the 'set' of labeled accounts to investigators for further monitored.


4. For the part of data cleaning, the previous agent's markdowns were incomplete and disaccord due to the internal handover issues. It require advanced text mining skills, which was the skill I was lack of. If I have the opportunities to spearhead the resemble project again, I will put more emphasis on the text preprocessing.( e.g, different language document and personal informations.)

5. The reported illegal account's trading records were classified into several clusters as the suspicious trading patterns(A set). Then we leverage K means++ to add an additional variable called cluster number for the monthly trading dataset after cleaning. After reshaping the dataset and grouping them as [countries - user base] (B set), we are able to utilize these two sets of data for further analysis.



**Here are several approaches and insights we adopted:**

1. Using K means ++ to distinguish the monthly trading record(which were grouped by userID beforehand)

2. The key point is to set the correct 'Rank' for the quantitative variables. And put more attention to the high frequency but low ranking(eg, trading amount) account. It requires several meetings with AML expertise.

3. Compare the similarity of the clustriods(represented as  vector position coordinates) of A set and B set. The way we used was the extract out the categorical variable from the vector and use Jaccard Sim. And for the vector without categorical variables, we simply normalize them and utilize cosine sim as measurement. The total distance of the clustriods were defined as the sum of Jaccard dist and cosine dist. Then we dived deeper into the cluster which had low total distance.

4. We set the different baselines for adjusting under the announcement of FATF. For example, for the user whose current living location (provided as KYC documents for current 3 months proof of living, ex, the electrical bill for matched Residential address and matched client full name) belongs to jurisdictions list get a higher baseline of risk. The safer countries get a lower baseline. The constant would fluctuate only between (0+,2-), and considered as a multiplier. Moreover, we use Selenium to automatically updated the project backend jurisdictions list to avoid the casting off from the FATF.

5. Link analysis should be applied on the suspicious cluster. However, we do not have enough time and information for that part.

6. The account with opened access  of FAIT Token like USDT could be money mule. And this kind of account might use the service of ' platform landing & borrow' to reach the goal of money laundry. With this concern, we have noticed our senior manager for the potential Money laundry risk, and the respone was " The FAIT account were subjected to stricter scrutiny than the normal accounts. And each business has its own risk appetite, what we do is to make a balance between the acceptable risk and the bargain."
