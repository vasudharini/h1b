9)register /usr/local/hive/lib/hive-exec-1.2.1.jar;
register /usr/local/hive/lib/hive-common-1.2.1.jar;
s1 = LOAD 'hdfs://localhost:54310/user/hive/warehouse/h1visa.db/h1b_final' USING PigStorage('\t') as (s_no:double,case_status:chararray,employer_name:chararray,soc_name:chararray,job_title:chararray,full_time_position:chararray,prevailing_wage:double,year:chararray,worksite:chararray,longitude,latitude);
s2= group s1 by employer_name;
s3= foreach s2 generate group,COUNT($1);

s4= FILTER s1 by case_status=='CERTIFIED';
s5= group s4 by employer_name;
s6= foreach s5 generate group,COUNT($1);

s7= FILTER s1 by case_status=='CERTIFIED-WITHDRAWN';
s8= group s7 by employer_name;
s9= foreach s8 generate group,COUNT($1);

s10= join s3 by $0, s6 by $0, s9 by $0;

s11= foreach s10 generate $0,$1,$3,$5;
s12= foreach s11 generate $0,(float)($2+$3)*100/($1),$1;
s13= FILTER s12 by $1>70 and $2>1000;
s14= order s13 by $1 DESC;
dump s14;





10)register /usr/local/hive/lib/hive-exec-1.2.1.jar;
register /usr/local/hive/lib/hive-common-1.2.1.jar;
s1 = LOAD 'hdfs://localhost:54310/user/hive/warehouse/h1visa.db/h1b_final' USING PigStorage('\t') as (s_no:double,case_status:chararray,employer_name:chararray,soc_name:chararray,job_title:chararray,full_time_position:chararray,prevailing_wage:double,year:chararray,worksite:chararray,longitude,latitude);
s2= group s1 by job_title;
s3= foreach s2 generate group,COUNT($1);

s4= FILTER s1 by case_status=='CERTIFIED';
s5= group s4 by job_title;
s6= foreach s5 generate group,COUNT($1);

s7= FILTER s1 by case_status=='CERTIFIED-WITHDRAWN';
s8= group s7 by job_title;
s9= foreach s8 generate group,COUNT($1);

s10= join s3 by $0, s6 by $0, s9 by $0;

s11= foreach s10 generate $0,$1,$3,$5;
s12= foreach s11 generate $0,(float)($2+$3)*100/($1),$1;
s13= FILTER s12 by $1>70 and $2>1000;
s14= order s13 by $1 DESC;
dump s14;
store s14 into '/home/hduser/niit/pig/question10' using PigStorage('\t');
