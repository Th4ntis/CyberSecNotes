# Fawn

![](<../../../.gitbook/assets/image (669).png>)

## ​Task 1

What does the 3-letter acronym FTP stand for? - `File Transfer Protocol`

## Task 2

What communication model does FTP use, architecturally speaking? - `client-server model`

## Task 3 <a href="#task-3" id="task-3"></a>

What is the name of one popular GUI FTP program? - `Filezilla`

## Task 4 <a href="#task-4" id="task-4"></a>

Which port is the FTP service active on usually? - `21 TCP`

## Task 5 <a href="#task-5" id="task-5"></a>

What acronym is used for the secure version of FTP? - `SFTP`

## Task 6 <a href="#task-6" id="task-6"></a>

What is the command we can use to test our connection to the target? - `ping`

## Task 7 <a href="#task-7" id="task-7"></a>

From your scans, what version is FTP running on the target? - `vsftpd 3.0.3`

## Task 8 <a href="#task-8" id="task-8"></a>

From your scans, what OS type is running on the target? - `Unix`

## Task 9 <a href="#task-9" id="task-9"></a>

Submit root flag - `035db21c881520061c53e0536e44f815`

We first FTP to the machine​

![](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAwjgRRQM65MtOamBB7Ci%2Fuploads%2FHTNJpDlCUVc7uQuAt3m2%2Fimage.png?alt=media\&token=7a47c4ff-615d-40a3-a155-8f926e8a14e4)

​After connecting we specify our user​

![](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAwjgRRQM65MtOamBB7Ci%2Fuploads%2FYUGxeI3DM1C8pbLFU4wU%2Fimage.png?alt=media\&token=2e890a95-f7c5-499a-ba30-2945f7eea57b)

Now we can look for files and download them.​

![](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAwjgRRQM65MtOamBB7Ci%2Fuploads%2F8ogAwMmIJNeNY4tvmKvW%2Fimage.png?alt=media\&token=77acf694-1d88-49a4-9b9e-0d118086c2a1)

After we download our flag.txt file, we exit the FTP session, and cat our file to reveal our flag.
