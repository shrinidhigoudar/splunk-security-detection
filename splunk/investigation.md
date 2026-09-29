# Splunk Investigation



## RDP Brute Force Investigation

After the alert was triggered, the events were investigated using:

- Account name

- Source network address

- Number of failed attempts

- Event timestamp

The search results were reviewed to determine whether multiple failed
authentication attempts originated from the same source.



## MSHTA Investigation

For MSHTA activity, the following information was reviewed:

- Process name

- Process command line

- Account

- Computer name

- Parent/creator process

- Event timestamp

This helped verify the process execution observed by the detection.

## Investigation Evidence

The screenshots in the `screenshots/` directory show the searches and

triggered events observed during the investigation.

