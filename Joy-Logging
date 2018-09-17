import datetime

today = datetime.date.today() #Sets today for opening that file from today.
time_of_day = datetime.datetime.now() #Sets time of day as now.

f = open('/home/LukeVenter/returned-twitter-data/main-twitter-data/%s.txt' % (today), 'r')
searchlines = f.readlines()
#f = the tweets for the day.

R = open("/home/LukeVenter/returned-twitter-data/stored-fear/Fear-For-%s.txt"  % (today),"a+")
#R = the file that only contains the tweets that expressed fear that day - lines here need to be counted.

S = open("/home/LukeVenter/returned-twitter-data/temp-files/Temp-Stored-Fear.txt", 'w')
#S = stored number of tweets to write to google sheet.

X = open("/home/LukeVenter/returned-twitter-data/temp-files/Temp-Stored-Joy.txt", 'w')
#X = stored number of tweets to write to google sheet.

Y = open("/home/LukeVenter/returned-twitter-data/stored-joy/Joy-For-%s.txt"  % (today),"a+")
#Y = the file that only contains the tweets that expressed joy that day - lines here need to be counted.

#Everything above here is a formality. The function is below.

def fear_count_stored(): #Supposed to count and store the number of tweets
		with open("/home/LukeVenter/returned-twitter-data/stored-fear/Fear-For-%s.txt"  % (today)) as fear_for_the_day:
#			print (sum(1 for _ in fear_for_the_day))
			S.write("%s" % sum(1 for _ in fear_for_the_day))
			S.close
#This def below is supposed to store the fear_count on the google sheet so that it can be represented in a graph.

def joy_count_stored(): #Supposed to count and store the number of tweets
#		with open("/home/LukeVenter/returned-twitter-data/stored-joy/Joy-For-2017-06-22.txt") as joy_for_the_day:
		with open("/home/LukeVenter/returned-twitter-data/stored-joy/Joy-For-%s.txt"  % (today)) as joy_for_the_day:
#			print (sum(1 for _ in joy_for_the_day))
			X.write("%s" % sum(1 for _ in joy_for_the_day))
			X.close

def write_to_sheet():

	import gspread
	from oauth2client.service_account import ServiceAccountCredentials

	scope = ['https://spreadsheets.google.com/feeds']
	creds = ServiceAccountCredentials.from_json_keyfile_name('/home/LukeVenter/auth-files/My-Project-XXXXXXXX.json', scope)
	client = gspread.authorize(creds)

	sheet = client.open("From-Py-To-Sheet").sheet1 #Open the sheet

	fline = open("/home/LukeVenter/returned-twitter-data/temp-files/Temp-Stored-Fear.txt", "r")
	jline = open("/home/LukeVenter/returned-twitter-data/temp-files/Temp-Stored-Joy.txt", "r")
	contents1 = fline.readline() #Fear
	contents2 = jline.readline() #Joy
	print ("Count:", contents1)
	print ("Count:", contents2)
	new_value1 = (contents1) #This needs to be the value presented in first line of the file.
	new_value2 = (contents2) #This needs to be the value presented in first line of the file.

	row = today,new_value1,new_value2

	sheet.append_row(row) #action the sheet append.

fear_count_stored()
S.close()
joy_count_stored()
X.close()
write_to_sheet()
