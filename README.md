For each App,PII pair we evaluate the "decision importance score" as such:

A = # of Allows

D = # of Denies

F = # of Fakes

|A - (D + F)| / (A + D + F)

For each App,PII pair we will therefore have a metric that will give a score close to 1 if most of the user decisions were allows and a -1 if most of the decisions were denies and fakes. Also if the decisions were close to split then you will get a number close to zero and as you will see later, this App,PII will have a lesser effect on the recommendations given.

This is a computation across all users. In the next step we will compute user scores using the above computed metrics.

For each user, we will create two scores: Allows Score and Deny/Fake Score

These will be computed as such:

Allow Score: Vector for most popular App,PII pairs with 1's at all the allows and 0 elsewhere. This is dot producted with the "decision importance" vector to get the allow score.

Deny/Fake Score: Vector for most popular App,PII pairs with 1's at all the denies or fakes and 0 elsewhere. This is dot producted with the "decision importance" vector to get the deny/fake score.

Both the scores would be normalized based on the location from which the decision is made. (For example Global allow has less value than manually going to an app and making the decision).

Now we have two scores for each user and we will apply a 2-d clustering into 3 clusters.

Ideally, the clusters should be separated as 2 outlier groups (containing 25% of users each) and one main group (containing 50% of the users). The bottom 2 groups would be nudged towards the decisions of their immediately superior group.


