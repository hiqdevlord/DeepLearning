


	con=dbConnect(MySQL(),user="root",password="mysql",dbname="ali")
	dbSendQuery(con,'SET NAMES utf8')
	res <- dbSendQuery(con,"select* from cityinfo")
	dat <- fetch(res,n=-1)