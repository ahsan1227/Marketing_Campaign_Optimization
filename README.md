# Marketing_Campaign_Optimization
An advertising promotion campaign was tested to see if it would be able to get more customers a newly launched product for $10. Since it costs the company $0.15 to send out each promotion, it would be best to limit that promotion only to those that are most receptive to the promotion to limit the cost and increase ROAS.

The data for this exercise consists of about 120,000 data points split in a 2:1 ratio among training and test files. It looks like this:

![image](https://github.com/ahsan1227/Marketing_Campaign_Optimization/assets/136532329/54e44b49-b827-4c12-9333-ce24cee2a950)

Each data point includes Promotion Column indicating whether or not an individual was sent a promotion for the product, and one column indicating whether or not that individual eventually purchased that product. Each individual also has seven additional features associated with them, which are provided abstractly as V1-V7.

Whether a customer received an ad, we can divide the customers into control group (didn't receive an ad) and experiment group (received an ad). In training data, each group has about 42000 data points and the purchase rates are 0.76% and 1.7% for control and experiment groups. Thus we can expect that one difficult task in this project is to handle data imbalance. We will run two separate machine learning models. One on the control group and one on the experimental group

![image](https://github.com/ahsan1227/Marketing_Campaign_Optimization/assets/136532329/fad6c04d-a757-4b3a-ab70-ce4d0e063aa7)

As we can see the instance of when the product was bought with a promotion or without is very less. Therefore we have to up sample that data to remove the bias in the model. Similary we downsample the data when the product was not bought.


Out goal is to maximize the following metrics:

1. **Incremental Response Rate (IRR):** IRR depicts how many more customers purchased the product with the promotion, as compared to if they didn't receive the promotion. Mathematically, it's the ratio of the number of purchasers in the promotion group to the total number of customers in the purchasers group (treatment) minus the ratio of the number of purchasers in the non-promotional group to the total number of customers in the non-promotional.

2. **Net Incremental Revenue (NIR):** NIR depicts how much is made (or lost) by sending out the promotion. Mathematically, this is 10 times the total number of purchasers that received the promotion minus 0.15 times the number of promotions sent out, minus 10 times the number of purchasers who were not given the promotion.

![image](https://github.com/ahsan1227/Marketing_Campaign_Optimization/assets/136532329/54b1cea4-951a-4a7c-b63b-c2b88ef52aca)

# Promotion Strategy

Our KPI's suggest that we are not just focusing on cutting down the cost of Ad Spent but also the conversions. This suggests that we should focus only those customers who are receptive of the promotional offer and not waste our dollars on customers that will buy the product even without seeing the add.

# Tuning the Model

When tuning the model, we focused mostly on the loss from errors rather than gainings from giving the ads to the right people. It actually worked quite well in the end. More details can be found in the docstring of the function evaluate. The reason why we didn't consider true positives here to "reward" the model is that when we trained the models, we greatly balanced the data --- we greatly upsampled the purchase group and only sample a little (no more than 10%) from non-purchase group , so we can expect that recall is usually higher than precision. In other words, our model might have done its best to recognize the customers who will make purchases but it can be over optimistic. We want to correct that since giving promotion ads to too many people can greatly increase the cost of the campaign.

# Results

Udacity provided a benchmark result for us to compare:

* irr: 0.0188
* nir: 189.45

Our Reuslts are show a distribution of IRR from 0.0175 to 0.02 which is very close to the benchmark. The NIR varies from 200 to 400 which is significantly higher owing to the targeted approach of only sending promotional offers to those customers who purchase the product after promotion

# Future improvement
More work needs to be done to make the code more efficient and simpler. I'll be doing more work in my free time to make this code easier to interpret as some parts of it might be a bit confusing.

