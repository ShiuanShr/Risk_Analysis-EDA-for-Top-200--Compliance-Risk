Preface:
We can only share partial final performance to prove the existance of the project because it contain clients personal information (trading amount, location, frequency, pattern cluster, trading cryptocurencies, etc.) Even though we have unlabeledized the data and replaced the privacy information with eligible ID, it still only allowed to be used for the purpose of  user experience improvement or for internal AML regulartory. Last but not the least, due to the current GDPR policy in our EU clients, the automatic profiling is no longer allowed without additional consent papers.

However, as a leader of this project, we could briefly talk about how we implement the project.

In the begining, it was EDA for risk report without precedent case.
The raw data is extremely dirty beyond our expectation.
After complex data cleaning process, and text mining preprocessing, we get  relative 'cleaned' monthly-based trading record datasets for over 50 countries Bitfinex served.
It was a massiveb scale dataset. Therefore, we random picked one country's dataset as the first profiling target and then applied the following data process on the rest of them after we construct the mature data pipeline.

To be brief, here are some illustrations for this tedious hunting game:

1. That was massive scale dataset, hence, only data pipeline was suitable for it. As the result, the project was conducted by python. However, the visualization part was required to use GoogleSilde for presentation due to the adminstrative manager's requires. Hence, in order to build the linkage between G-sildes and G-spreadsheet, after all the data analysis works, we have to extract the data, plot we want via data pipeline and load only a limited size into google spreadsheet because spreadsheet did not support the API we needed. However, for the trial demo, we use simply Excel, Google Spreadsheet directly for concept demonstration.

2. Most of data are noises, therefore, certained degree of feature engineer helps. However, most of time, the important variables depends on what AML expertise told us.

3. It contains lots of idle accounts, which trading frequency almost equal to 0. This kind of accounts increased the sparse level of data. But can not be discard due to the probability of the head accounts. Moreover, the criminal account would not exist alone, mostly, they would use plenty head accounts to make the source invisible. And have to say, under property of blockchain, it would be almost unlikly to trace  for outsider (Gov AML related Competent Authority) if the investigators or risk analysts in crypto exchange are neglected of duty. Back to the topic, what we did is to point out  'sets' of accounts having highly suspecious trading relationship from  million trading record and turn over the 'set' of labeled accounts to investigators for further monitored.  

3. For the part of data cleaning, the previous agent's markdowns were incomplete and disaccord due to the internal handover issues. It require advanced text mining skill, which was the skill I was lack of. If let me re-spearhead the project again, I will put more emphasize on the text variable preprocessing.

4. The reported illigal account's trading record were  classified into several clusters as the suspecious trading patterns(A set). Then we leverage K means++ to add an additional variable called clusterNumber for the monthly trading dataset after cleaning. After reshaping the dataset and group them as countries - user base (B set), we utilze this two set of data do the further analyse.

Here are serveral approachs and insights we adopted:

1. Using K means ++ to distinguish the monthly trading record(which were grouped by userID beforehand)

2. The key point is to set the correct 'Rank' for quantitative variable. And put more attention to the high frequency but low ranking(eg, trading amount) account. It requires several meeting with AML expetise.

3. Compare the similarity of the clustriod(as a vector position coordinate) of the k means of A set and B set. The way we used was the extract out the categorical varible from vector and using Jaccard Sim. And for the vector without categorical varible, we simplily normalize them and utilze cosine sim as  measurement. The total distance of the clustriod were defined as the sum of Jaccard dist and cosine dist. Then we dived more deeper into the cluster which having low total distance.

4. We set the different baseline for adjusting under the announcement of FATF. For example, for the user whose current living location (provided as KYC documents for current 3 months proof of living, ex,electrical bill for matched Residential address and matched client full name) belongs to jurisdictions list get a higher baseline of risk. The safer countries get lower baseline. The constant would fluctuate only between (0+,2-), and considerd as a multiplier. Moreover, we use Selenium to automatically updated the project backend jurisdictions list to avoid the casting off from the FATF.



