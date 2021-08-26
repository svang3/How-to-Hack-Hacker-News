# How-to-Hack-Hacker-News

/* read into the data and pick the top five stores with highest score */
select title, score
from hacker_news
order by score desc
limit 5;

/* find the toal score of all the stories */
select sum(score)
from hacker_news;

/* find the individual users who have scores more than 200 */
select user, sum(score)
from hacker_news
group by user
having sum(score) > 200
order by 2 desc;

/* combine scores together and divide by the total sum */
select (517 + 309 + 304 + 282) / 6366.0;

/* search for the total user who posted the link */
select user, count(*)
from hacker_news
where url like '%watch?v=dQw4w9WgXcQ%'
group by user
order by count(*) desc;

/* categorize each story based on their source and add column for the number of stories*/
select case
   when url like '%github.com%' then 'GitHub'
   when url like '%medium.com%' then 'Medium'
   when url like '%nytimes.com%' then 'New York Times'
   else 'Other'
  end as 'Source',
  count(*)
from hacker_news
group by 1;

/* check the timestamp column to look at the format */
select timestamp
from hacker_news
limit 10;

/* return a formatted date */
select timestamp,
   strftime('%H', timestamp)
from hacker_news
group by 1
limit 20;

/* return columns of hours, avg score, and count stories for each hour */
select strftime('%H', timestamp) as 'Hour', 
   round(avg(score), 1) as 'Average Score', 
   count(*) as 'Number of Stories'
from hacker_news
where timestamp is not null
group by 1
order by 1;
