# datares_2021_streamingservices
## Section 1: Genre over time 
## Line graph, y-axis: year, x-axis: number of shows

Genre_Dataset %>% count(Year,Genre)
genre <- Genre_Dataset %>% count(Year,Genre) %>%
  ggplot()+geom_line(aes(x=Year,y=n,col=Genre)) 
genre + ggtitle("Number of shows on Netflix and Prime per year by genres") +
xlab("Year") + ylab("Number of shows") 

## Bar Plot

genres <- ggplot(Genre_Dataset, aes(fill=Genre , x=Year)) +
  geom_bar()
genres + ggtitle("Number of shows on Netflix and Prime per year by genres") +
  xlab("Year") + ylab("Number of shows")

## Section 2: Ranking over Time 
## Scatter Plot between Ranking of Genre over time

na.omit(Genre_Dataset)
ggplot(Genre_Dataset, aes(x=Year, 
                          y=IMDb, color=Genre)) + geom_point()


## Box Plot show the IMDb score vs Genre

boxplot(IMDb ~ Genre, data = Genre_Dataset, 
        col = "#DF536B", main = "IMDb Score by Genre")


## Section 3: Viewership overtime (Movie/TV Show)
## Line graph: Year, type

Netflix %>% count(release_year,type)
view <- Netflix %>% count(release_year,type) %>%
  ggplot()+geom_line(aes(x=release_year,y=n,col=type))


## Bar plot
view <- ggplot(Netflix, aes(fill=type , x=release_year)) +
  geom_bar()
view + ggtitle("Number of shows on Netflix and Prime per year") +
  xlab("Year") + ylab("Number of shows")

## Section 4: Number of shows on each platform over time
## Line graph: Year, Number of shows


dt2 <- subset(Streaming, Netflix>0)
dt2 %>% count(Year,Netflix)
netflix <- dt2 %>% count(Year,Netflix) %>%
  ggplot()+geom_line(aes(x=Year,y=n,col=Netflix))
netflix


dt3 <- subset(Streaming, Hulu>0)
dt3 %>% count(Year,Hulu)
hulu <- dt3 %>% count(Year,Hulu) %>%
  ggplot()+geom_line(aes(x=Year,y=n,col=Hulu))
hulu


dt4 <- subset(Streaming, Prime>0)
dt4 %>% count(Year,Prime)
prime <- dt4 %>% count(Year,Prime) %>%
  ggplot()+geom_line(aes(x=Year,y=n,col=Prime))
prime


dt5 <- subset(Streaming, Disney>0)
dt5 %>% count(Year,Disney)
disney <- dt5 %>% count(Year,Disney) %>%
  ggplot()+geom_line(aes(x=Year,y=n,col=Disney))
disney

grid.arrange(
  netflix,hulu,prime,disney,
  nrow = 2,
  top = "Number of shows on each platform per year"
  )
)






