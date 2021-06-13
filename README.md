# soal-shift-sisop-modul-4-I07-2021

Made by:

Group I07

Gede Yoga Arisudana (05111942000009)

Salma Rahma Lailia (05111942000016)

Zulfiqar Rahman Aji (05111942000019)



## PROBLEM 1

In problem 1, we need to encode or decode a directory using Atbesh Cipher method, and the following method look like this
```
void atbash(char *str, int start, int end) 
{
    for (int i = start; i < end; i++) 
    {
        if (str[i] == '/') 
            continue;
        if (i != start && str[i] == '.') 
            break;
 
        if (str[i] >= 'A' && str[i] <= 'Z')
        {
            str[i] = 'Z' + 'A' - str[i];
        }
        else if (str[i] >= 'a' && str[i] <= 'z')
        {
            str[i] = 'z' + 'a' - str[i];
        }
    }
}
```
Using the algorithm above, we can encode or decode our directory or file name, for the encode function will look like this
```
void encode(char *str) 
{
    if (!strcmp(str, ".") || !strcmp(str, "..")) 
        return;
    atbash(str, 0, strlen(str));
 
    printf("==== enc:atb:%s\n", str);
}
```
After we encode the directory or file name, it will changed according to the Atbash Cipher algorithm. We can also decode it, to maka the directory or file name back to it's former name, and the decode function will look like this
```
void decode(char *str) 
{
    int s=0,i;
    if (!strcmp(str, ".") || !strcmp(str, "..")) 
        return;
    if (strstr(str, "/") == NULL) 
        return;
 
    int str_length = strlen(str);
    for (i = str_length; i >= 0; i--) 
    {
        if (str[i] == '/') 
            break;
 
        if (str[i] == '.') 
        {
            str_length = i;
            break;
        }
    }
    for (i = 0; i < str_length; i++) 
    {
        if (str[i] == '/') 
        {
            s = i + 1;
            break;
        }
    }
 
    atbash(str, s, str_length);
    printf("==== dec:atb:%s\n", str);
}
```
We must also make a log for every action that we make.

## PROBLEM 2


## PROBLEM 3


## PROBLEM 4

In problem 4, we are needed to make a log system for each number. But, we only make it for number 1, because we only do number 1. First, we will make a function so the log will be divided into 2 type (INFO and ERROR), and the function will look like this
```
void logType(char *str, int type) 
{
    FILE *log_file = fopen(logpath, "a");
 
    time_t current_time;
    time(&current_time);
    struct tm *time_info;
    time_info = localtime(&current_time);
 
    if (type == INFO) 
    {
        fprintf(log_file, "INFO::%d%d%d-%d:%d:%d:%s\n", time_info->tm_mday,
                time_info->tm_mon, time_info->tm_year, time_info->tm_hour,
                time_info->tm_min, time_info->tm_sec, str);
    } 
    else if (type == WARNING) 
    {
        fprintf(log_file, "WARNING::%d%d%d-%d:%d:%d:%s\n", time_info->tm_mday,
                time_info->tm_mon, time_info->tm_year, time_info->tm_hour,
                time_info->tm_min, time_info->tm_sec, str);
    }
}
```
To open and write in the log system we will also make a function for it, and it will look thiws
```
void logs1(char *from, char *dest) 
{
    int i;
    for (i=strlen(dest); i >= 0; i--) 
    {
        if (dest[i] == '/') 
            break;
    }
    if (strstr(dest + i, ATOZ) == NULL) 
        return;
 
    FILE *log_file = fopen(logpath, "a");
    fprintf(log_file, "%s -> %s\n", from, dest);
}
```
Therefore, with this functions the log message will be written in the log system
