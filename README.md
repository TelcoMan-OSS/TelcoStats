# Who am I

Hi! My name is Sjoerd. I work for a telecoms equipment provider. My day job consists out of resolving large network issues around mobile phone towers. I do both physical engineering and virtual. Sometimes I get to climb on Cell Sites (Those big towers) to check what's going on with our equipment. Pretty cool huh?!

# What is this project

I wanted to give people more public access to actual statistics measured in a controlled environment. a lot of our clients such as Vodafone try to prevent these statistics from being public knowledge as they are afraid of reputation damage etc. I also like seeing how MVNOs compare to the larger providers.

# Lets dive into the details

My test setup is a controlled environment in my home. The phone is on a stand, free of obstructions. For all tests we use either LTE or UMTS.

The test setup settings are as follows, but can differ based on each provider

NAS.GUTI: m_tmsi:0, mmec: 0, mmegi: 0
Serving Cell Info: dl_bw: 50,freqband:20,sel_plmn_mnc:8

Depending on the day, our service Cell MEAS is:
rsrp1: -110
rsrq1: 24
rsrp1: -110
sinr0: 1.0

# Poor performance by MVNOs in NL

Most MVNO's in the Netherlands have a very poor performance ratio. This is as they are trying to route over "breath-first" connections. This means that providers such as Lebera, Voiceworks, belsimpel, etc. try to have as much people using the same ratio. this causes connections issues when calling (having to repeat a dail), but also results in large performance issues when using data connections.

NVMOs often proudly say "We are using Network X of a large provider". This is also untrue. They are allowed to use a subset of the bandwidth and frequency range of that provider. This does not mean they have the same coverage or performance. 

A good example of this is Ben, Ben uses the T-Mobile network, but is only allowed specific frequencies, the so called "MVMO-subrange" as we call it. This means that while T-Mobile has 100% 4G coverage, Ben only has 65% across all of the Netherlands. MVMOs can pay for a higher frequency range but on average do not. This means MVMOs never have the full coverage their (mother) provider does.

# Call Statistics

The following statistics have all been made with the same phone, in the same location, over the course of several months. The phone uses an auto-dailer to dail once every 10 minutes for 30 days, or until 4.320 calls have been made. The auto-dailer tries to keep the connection open for 1 minute, and registers if the call ends before that time.

| Provider   | Calls failed to initiate | Call succesfully intiated | Call ended naturally | Calls ended abruptly | Total Calls |
|------------|--------------------------|---------------------------|----------------------|----------------------|-------------|
| Vodafone   | 15                       | 4.305                     | 4.305                | 0                    | 4.320       |
| T-Mobile   | 29                       | 4.291                     | 4.289                | 2                    | 4.320       |
| KPN        | 1                        | 4.319                     | 4.319                | 0                    | 4.320       |
| Ben        | 152                      | 4.168                     | 4.140                | 28                   | 4.320       |
| DeanOne    | 31                       | 4.289                     | 4.289                | 0                    | 4.320       |
| Voiceworks | 582                      | 3.738                     | 3.398                | 340                  | 4.320       |
| RoutIT     | 391                      | 3.929                     | 3.929                | 0                    | 4.320       |
| Lebera     | 23                       | 4.297                     | 4.296                | 1                    | 4.320       |
| Simpel     | 230                      | 4.090                     | 4.001                | 89                   | 4.320       |
| Tele2      | 1                        | 1.984                     | 1.984                | 0                    | 1.985       |

Currently the Tele2 test is still ongoing. Other tests have been completed. As you can see, the primary providers(Vodafone, T-Mobile, KPN) have an expected loss ratio of less than 1%. This is to be expected as they are maintaining the critical network components for our country as well.

The NVMOs on the other hand have a *very* large dropout percentage. I've researched these in-depth and have a couple of comments per provider:

Ben: Ben has a maintenence cycle between 04:00 and 05:00 in my area. This means more dropout is to be expected at these times. This could be resolved by better failover and splitting maintence cycles better.

Voiceworks: Voiceworks is by far the worst performing MVNO and I'd advise people to stay away from this MVNO. Every day between 06:00 and 09:00 calls start dropping. I expect that this is due to their platform not handling the morning rush and load balancing this evenly. Voiceworks is also the only provider that we see our 1 minute calls ending before-hand. We've also seen this issue between 01:00 and 04:00 at times, where we expect it to be a maintenence cycle. There is no excuse to have so much downtime for a voice provider, which can be regarded as a critical service.

RoutIT: Same as Voiceworks. The amount of dropped calls is much lower, but the count of calls that do not go through at all and require a redial is extremely high.

Simpel: Simpel does not have enough capacity in the evenings. We've seen calls fail from 17:00 to 20:00, but not at other times. These are also the moments when dials start failing.

# data performance

I am currently setting up a data testing platform, which is more difficult as we have to account for each providers frequence range and promised performance. I will create a new repo for this.

# so now what?

I hope people can use these statistics for something. I for one find it super intresting from a network management perspective. :)
