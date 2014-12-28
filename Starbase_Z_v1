# STARBASE Z
# Version 1
# (c) 2014, Jeff Pettineo

# spacedock function ` line 365
# combat routine ~ line 600 

mywep = 50
mydefence = 50
myhull = 100
myfame = 0
mycredits = 250
mypilot = 0
mydiplomacy = 0
myscieng = 0
myhitchance = 0
scieng = 0
myrank = 0
myname = 0
justdied = False

skillpoints = 50

enemyhull = 0
enemypilot = 0
enemydef = 0
enemydefence = 0
enemywep = 0
enemyhitchance = 0

addfame = 0
addcredits = 0
addpilot = 0
adddiplom = 0
addscieng = 0
alienrace = 0
alienvar = 0

diplomacyroll = 0
diplomchoice = 0

totalbattles = 0
totalconflicts = 0
myship = 0
pointstomaxsci = 100 - myscieng
pointstomaxdip = 100 - mydiplomacy
pointstomaxpilot = 100 - mypilot
ejected = 0

highscorenow = 0
scorestally = []
finalscore = 0
sleepytime = .25
sim = False
battlespeed = 1

from random import randint
import pickle
import time
import os

def saveorload():
	global myhull
	global mywep
	global mycredits
	global mypilot
	global mydiplomacy
	global myscieng
	global myfame
	global myname
	global myship
	global myrank
	
	print "Would you like to LOAD (L) a saved game, or ..."
	print "create a NEW GAME (N)"
	firstchoice = raw_input(' >')
	if firstchoice == "N" or firstchoice ==	"n":
		introduction()
	elif firstchoice == "L" or firstchoice == "l":
		with open('savefile.dat', 'rb') as f:
			mypilot, mydiplomacy, myscieng, myhull, mywep, mycredits, myrank, myfame, myname, myship = pickle.load(f)
			spacedock()
	else:
		saveorload()
	
def clearscreen():
	import os			
	os.system('cls')
	
def speed():
	global battlespeed
	global sleepytime
	print "Enter the speed of your battle reports: 1 [Slowest] to 5 [Fastest]"
	try:
		battlespeed = int(raw_input('> '))
	except ValueError:
		speed()
	else:
		if battlespeed > 6 or battlespeed == 0:
			print "Please enter a speed capable of being processed by a human nervous system."
			speed()
		else:
			print "Your speed is now %d" % (battlespeed)
			sleepytime = battlespeed/(battlespeed*battlespeed)
			spacedock()
			
def specialization():	
	global mypilot
	global myscieng
	global mydiplomacy 
	global skillpoints
	
	print """\n
	You have been granted some time in the Virtual Training Simulator (VTS). 
	The VTS will provide 50 points' worth of training to you free of charge.
	In the future, you will have to pay for additional training."""
	time.sleep(1)
	print """\n Remember, the maximum a rating can reach in any one area is 100.
	\n You begin with %d PILOTING, %d DIPLOMACY and %d SCIENG 
	\n How many points would you like to add to your PILOTING skill: (between 0 and 50 points)? """ % (mypilot, mydiplomacy, myscieng)
	
	try:
		pilotskillpoints = int(raw_input('> '))
	except ValueError:
		specialization()
	else:
		if pilotskillpoints < skillpoints and pilotskillpoints >= 0:
			skillpoints = skillpoints - pilotskillpoints
			mypilot += pilotskillpoints
			print "Your pilot skill rating is now %d." % (mypilot)
			diplomacyeng()
		elif pilotskillpoints == skillpoints:
			mypilot = mypilot + pilotskillpoints
			mydiplomacy = mydiplomacy
			myscieng = myscieng
			initialreport()
		else:
			mypilot = mypilot
			myscieng = myscieng
			mydiplomacy = mydiplomacy
			skillpoints = skillpoints
			specialization()			
			
def diplomacyeng():
	global mypilot
	global myscieng
	global mydiplomacy
	global skillpoints
	global diplomacyskillpoints
	
	print """
	Now, let's train in DIPLOMACY.
	\n
	Please select the amount of training you wish to receive in DIPLOMACY.
	\n
	You have %d skill points available""" % (skillpoints)
	
	try:
		diplomacyskillpoints = int(raw_input('> '))
	except ValueError:
		diplomacyeng()
	else:
		if diplomacyskillpoints <= skillpoints and diplomacyskillpoints >= 0:
			mydiplomacy += diplomacyskillpoints
			skillpoints -= diplomacyskillpoints
			myscieng += skillpoints
			print """Your DIPLOMACY skill rating is now %d \n
			Your SCIENG is now %d.
			""" % (mydiplomacy, myscieng)
			initialreport()
		elif diplomacyskillpoints > skillpoints:
			diplomacyeng()
		
def initialreport():
	global mypilot
	global myscieng
	global mydiplomacy
	print """Your ratings are the following ...
	PILOTING....... %d
	DIPLOMACY ..... %d
	SCIENG......... %d\n
	Excellent!\n Let's move on...""" % (mypilot, mydiplomacy, myscieng)

def generate_enemy():
	global mywep
	global mydefence
	global myhull

	global myfame
	global mycredits

	global mypilot
	global myscieng
	global mydiplomacy
	global skillpoints
	
	global enemywep
	global enemyhull
	global enemypilot
	
	global addfame
	global addcredits
	global addpilot
	global adddiplom
	global addscieng
	
	alienrace = ["Zoz", "Megon", "Vorg"]
	shipclass = ["Scout", "Corvette", "Frigate"]
	alienvar = randint(0,2)
	shipvar = randint(0,2)
	print "you face a %s %s" % (alienrace[alienvar], shipclass[shipvar])
	if alienrace[alienvar] == "Zoz":
		enemywep = mywep
		enemydef = mydefence
		enemypilot = mypilot
		enemyhull = myhull
		addcredits = randint(100,200)
		addfame = randint(5,15)
		addpilot = randint(2,5)
		#enemyloot -- TBD
		# hullbonus
		print """ The %s %s zooms toward you.  You scan the ship and find that its ratings are the following:,
		|| Weapons %d || 
		|| Defence %d || 
		|| Hull Rating %d ||
		|| Enemy Experience Level %d ||
		""" % (alienrace[alienvar], shipclass[shipvar], enemywep, enemydef, enemyhull, enemypilot) 
		#battlesim()
		checkfordiplomacy()
	elif alienrace[alienvar] == "Megon":
		enemywep = mywep / 2
		enemydef = mydefence / 2
		enemypilot = mypilot / 2
		enemyhull = myhull / 2
		addcredits = randint(50,100)
		addfame = randint(5,10)
		addpilot = randint(2,5)
		# enemyloot -- TBD
		# hullbonus
		print """ The %s %s zooms toward you.  You scan the ship and find that its ratings are the following:,
		|| Weapons %d || 
		|| Defence %d || 
		|| Hull Rating %d ||
		|| Enemy Experience Level %d ||
		""" % (alienrace[alienvar], shipclass[shipvar], enemywep, enemydef, enemyhull, enemypilot) 
		#battlesim()
		checkfordiplomacy()
	elif alienrace[alienvar] == "Vorg":
		enemywep = mywep + (.1*mywep)
		enemydef = mydefence + (.2*mydefence)
		enemypilot = mypilot + (.2*mypilot)
		enemyhull = myhull
		addcredits = randint(100,200)
		addfame = randint(5,15)
		addpilot = randint(2,5)
		# enemyloot
		# hullbonus
		print """ The %s %s zooms toward you.  You scan the ship and find that its ratings are the following:,
		|| Weapons %d || 
		|| Defence %d || 
		|| Hull Rating %d ||
		|| Enemy Experience Level %d ||
		""" % (alienrace[alienvar], shipclass[shipvar], enemywep, enemydef, enemyhull, enemypilot) 
		#battlesim()
		checkfordiplomacy()
		# enemyloot -- TBD
		# hullbonus
	return alienvar

def info_Zoz():
	print """ 
	The Zoz are a war-like culture, known for aggressive attacks along disputed territories.
	Their defensive capabilities are average, but they possess advanced weapon amplification
	derived from the element Endurium, native to their homeworld.
	They are unlikely to retreat, even when facing insurmountable obstacles in battle. 
	"""
	
def info_Megon():
	print """
	The Megon are a a highly evolved culture, though  known to be more meditative in nature. 
	They will not attack unless provoked.  They are more interested in increasing the extent of their trade routes 
	as well as scientific advancement. They possess average weaponry and defensive capabilities.
	"""
	
def info_Vorg():
	print """
	Intelligence on the Vorg is still being gathered. At this point, the intelligence community only knows that
	the Vorg have extremely well developed shield and hull technology.  There are some reports that the Vorg have
	also been experimenting with mind-control training as an alternative to physical violence.
	"""

def operations():
	print """
	1) Training
	2) Repair
	3) Retire
	4) Save Game
	5) Return to Dock"""
	opchoice = raw_input('>')
	if opchoice == "1":
		training()
	elif opchoice == "2":
		repair()
	elif opchoice == "3":
		print "Do you really wish to give up this life of glorious zap zap! - Y or N?"
		retirechoice = raw_input('>')
		if retirechoice == "y" or retirechoice == "y" or retirechoice == "yes" or retirechoice == "YES":
			retire()
		else:
			operations()
	elif opchoice == "4":
		savegame()
	elif opchoice == "5":
		spacedock()
	else:
		operations()
		
	
def intel():
	print """
	1) Status Report
	2) Information
	3) Return to dock"""
	intelchoice = raw_input('>')
	if intelchoice == "1":
		status()
	elif intelchoice == "2":
		inform()
	elif intelchoice == "3":
		spacedock()
	else:
		intel()

#def settings():
#	print """
#	1) Save Game
#	2) Set Speed of Reports
#	3) Return to dock"""
#	settingschoice = raw_input('>')
#	if settingschoice == "1":
#		savegame()
#	elif settingschoice == "2":
#		speed()
#	elif settingschoice == "3":
#		spacedock()
#	else:
#		settings()		
	
def death():
	global mycredits
	global justdied
	global ejected
	global mywep
	global myhull
	global myfame
	global mydefence
	
	print """\n It's an unfortunate occurrence, but it happens... in the depths of space your ships has been torn apart by the ... 
	
	depths of the white-hot intensity of a "Zap-Zap" (TM) laser beam. 
	
	You sulk for a few days over the loss of your ship and the poor living conditions aboard your escape craft. That is, you started to stink after some time.
	
	You return to Starbase Z, but your commanders have deducted %d credits from your account, leaving you with nothing.
	
	But you have a new ship, forget your loss, and are determined to continue.""" % (mycredits)
	
	justdied = True
	mywep = 50
	mydefence = 50
	myhull = 100
	myfame = 0
	mycredits = 0
	ejected += 1
	
	christen()


def spacedock():
	global myscieng
	global mypilot
	global mydiplomacy
	
	global mycredits
	global myhull
	global mywep
	
	global myfame
	global myname
	global myship
	global myrank
	
	print """
	You have the following options:
		1 - VOYAGE .......(Zap Aliens & Get Loot)
		2 - OPERATIONS ...(Repair, Retire, Save Game, Train)
		3 - INTEL ........(Status, Info)
		What would you like to do?
	"""
	dockchoice = raw_input(' >')
	if dockchoice=="1":
		voyage()
	elif dockchoice=="2":
		operations()
	elif dockchoice=="3":
		intel()
	else:
		spacedock()
		
def savegame():
	with open('savefile.dat', 'wb') as f:
		pickle.dump([mypilot, mydiplomacy, myscieng, myhull, mywep, mycredits, myrank, myfame, myname, myship], f, protocol=2)
		print "SAVING "
		for i in range(5):
			i +=1
			print " .",
			time.sleep(.5)
		print "GOODBYE!"
		exit()

def rank():
	global myfame
	myrank = 0
	
	if myfame < 25 and myfame >= 0:
		myrank = 'ENSIGN'
		print "\nYou have achieved the rank of %s\n" % (myrank)
	if myfame < 50 and myfame > 25:
		myrank = 'LIEUTENANT'
		print "\nYou have achieved the rank of %s\n" % (myrank)
	if myfame < 100 and myfame > 50:
		myrank = 'COMMANDER'
		print "\nYou have achieved the rank of %s\n" % (myrank)
	if myfame < 250 and myfame > 100:
		myrank = 'CAPTAIN'
		print "\nYou have achieved the rank of %s\n" % (myrank)
	if myfame < 500 and myfame > 250:
		myrank = 'COMMODORE'
		print "\nYou have achieved the rank of %s\n" % (myrank)
	if myfame < 1000 and myfame > 500:
		myrank = 'REAR ADMIRAL'
		print "\nYou have achieved the rank of %s\n" % (myrank)
	if myfame > 1000:
		myrank = 'ADMIRAL'
		print "\nYou have achieved the rank of %s\n" % (myrank)
	
def retire():
	global mypilot
	global mydiplomacy
	global myscieng
	global totalbattles
	global totalconflicts
	global mycredits
	global myship
	global myfame
	global ejected
	
	print """\nYou have amassed wealth in the amount of %d credits.
	\nYou are retiring with the following ability levels:
	\t Piloting ..... %d
	\t Diplomacy .... %d
	\t SciEng........ %d
	\nYour ship, the %s, has fought through %d battles.
	\nYou have resolved conflict peacefully %d times
	\n You have abandoned ship %d times""" % (mycredits, mypilot, mydiplomacy, myscieng, myship, totalbattles, totalconflicts, ejected)
	if totalconflicts >= 3:
		print "\t\n You should be proud that you attempted to resolve at least a few matters peaceably."
	if totalbattles >= 10:
		print "\t\n Your skill in combat is impressive. Now take it easy."
	finalscore = mypilot + mydiplomacy + myscieng + (totalbattles*10) + (totalconflicts*10) + (myfame*10)
	rank()
	print "\t\nYour FINAL SCORE is ..... %d" % (finalscore)
	# checkforhigh()
	exit()
		
def status():
	global myhull
	global mypilot
	global mywep
	global mydiplomacy
	global mycredits
	global myfame
	global myname
	global myship
	print "STATUS REPORT:\n"
	print "Captain %r of the %r, here is your report..." % (myname, myship)
	print "HULL ...............%d\nWEP.................%d\nCREDITS.............%d\nPILOTING............%d\nDIPLOMACY...........%d\nSCIENG..............%d\nFAME................%d" % (myhull, mywep, mycredits, mypilot, mydiplomacy, myscieng, myfame)
	rank()
	intel()
	
def inform():
	print """
	What would you like to know?
	1 - Info on alien enemies
	2 - Your ship status
	3 - Information on shopping, repairs, and training rates
	4 - Return to the spacedock
	"""
	
	inform_choice = raw_input(' >')
	if inform_choice == "1": 
		info_Zoz()
		time.sleep(1)
		info_Megon()
		time.sleep(1)
		info_Vorg()
		time.sleep(1)
		inform()
	elif inform_choice == "2":
		status()
	elif inform_choice == "3":
		general_info()
	elif inform_choice == "4":
		spacedock()
	else:
		inform()
	
def general_info():
	print """
	\t\nThe station crew can repair your ship at one credit per one rating of hull integrity 
	\t\nThe Training Simulator is available for use at a reasonable price.
	\t\nThe Emporium, "Space Toys" (opening July 2214), offers equipment in the form of upgrades, armor, and weapons at varying prices.
	"""
	inform()
	
def voyage():
	generate_enemy()
	combatroutine()
	
def shop():
	print """
	UNDER 
	CONSTRUCTION 
	
	Grand Opening Expected:
	July 2214!!
	"""
	spacedock()

def repair():
	global myhull
	global mycredits
	global myscieng
	global mywep
	addscieng = randint(1,6)
	addwep = randint (1,5)
	repairneeds = 100 - myhull
	if mycredits == 0:
		print "\nYou are broke."
		print "\nThink about exploring to acquire more credits."
	print "\nScanning hull integrity ..... %d " % (myhull)
	if myhull == 100:
		print "\nYou have no need for repairs at this time."
		spacedock()
	elif mycredits < repairneeds:
		print "You cannot afford this service at this time."
		spacedock() 
	else:
		print "You will need %d credits to repair your hull in full" % (repairneeds)
		print "Would you like to repair your ship? Y or N?"
		repairyn = raw_input(' >')
		if repairyn == "Y" or repairyn == "y":
			mycredits = mycredits - repairneeds
			myhull = myhull + repairneeds
			myscieng = myscieng + addscieng
			mywep = mywep + addwep
			checkskills()
			print "\nYou now have %d credits and %d hull." % (mycredits, myhull)
			print "\nYour SCIENG skill has increased to %d." % (myscieng)
			print "\nYour WEP rating has increased to %d." % (mywep)
			spacedock()
		else:
			spacedock()
	#add a skill gain for scieng here! 
	# then do checkskills()

def targetkilled():
	global mycredits
	global mypilot
	global myfame
	global totalbattles
	
	import os
	os.system('cls') 
	print "VICTORY"
	print "From the salvageable cargo, you receive %d credits" % (addcredits)
	mycredits = mycredits + addcredits
	print "\n You now have %d credits in your stash" % (mycredits)
	mypilot = mypilot + addpilot
	myfame = myfame + addfame
	checkskills()
	print "\nIn addition, your pilot skill has increased to %d " % (mypilot)
	print "\nFor your heroic efforts, your fame has increased by %d. It is now %d" % (addfame, myfame)
	totalbattles += 1
	spacedock()
		
def combatroutine():
	global myhull
	global enemyhull
	global enemypilot
	global mypilot
	global mywep
	global enemywep
	global totalbattles
	global sim
	global sleepytime
	global battlespeed
	
	while myhull > 0:
		os.system('cls')
		print "Enemy hull is at %d percent \n" % (enemyhull)
		print "Your hull is at %d percent. \n" % (myhull)
		print "Fire!"
		time.sleep(sleepytime)
		myhitchance = 100 * (float(mypilot) /  float(mypilot + enemypilot)) 
		print "Your hit chance is %d " % (myhitchance)
		time.sleep(sleepytime)
		hitroll = randint(1,100)
		print "your hit roll is %d" % (hitroll)
		time.sleep(sleepytime)
		if hitroll <= myhitchance and hitroll <= .15*myhitchance:
			enemydmg = (.1*mywep)*2
			time.sleep(sleepytime)
			print "\n\t*** CRITICAL HIT! ***"
			time.sleep(sleepytime)
			print "\n\tYou do %d damage." % (enemydmg)	
			enemyhull = enemyhull - enemydmg
			print "Enemy hull is at ................ %d" % (enemyhull)
			time.sleep(sleepytime)
		elif hitroll <= myhitchance:
			enemydmg = .1*mywep
			print "*** You hit! ***"
			time.sleep(sleepytime)
			print "\n\t You do %d damage." % (enemydmg)
			enemyhull = enemyhull - enemydmg
			time.sleep(sleepytime)
			print "Enemy hull is at ................ %d" % (enemyhull)
		else:
			time.sleep(sleepytime)
			print "You missed! \n"
			time.sleep(sleepytime)
			print "Enemy hull is at ................ %d" % (enemyhull)
			time.sleep(sleepytime)
		print "\n"
		time.sleep(sleepytime)
		print "Enemy fires."
		enemyhitchance = 100 * (float(enemypilot) / float(enemypilot + mypilot))
		time.sleep(sleepytime)
		print "Enemy hit chance is %d " % (enemyhitchance)
		hitroll = randint(1,100)
		time.sleep(sleepytime)
		print "Enemy hit roll is %d" % (hitroll)
		if hitroll <= enemyhitchance:
			mydmg = .1*enemywep
			time.sleep(sleepytime)
			print "Enemy hit!"
			time.sleep(sleepytime)
			print "Enemy vessel does %d damage." % (mydmg)
			myhull = myhull - mydmg
			time.sleep(sleepytime)
			print "Your hull is at ................ %d" % (myhull)
		else:
			time.sleep(sleepytime)
			print "Enemy missed!"
			time.sleep(sleepytime)
			print "Your hull is at ................ %d" % (myhull)
		if enemyhull <= 0:
			time.sleep(sleepytime)
			print "Target Destroyed!"
			targetkilled()
		elif myhull <= 0:
			death()
		else: 
			if sim == False:
				anykey()
	spacedock()

def introduction():
	global myname
	global myship
	print """
	*****   STARBASE Z     *****
	***** 	(C) 2014       *****
	***** by Jeff Pettineo *****
	\n
	Welcome to Starbase Z.  Please report for duty.
	"""
	print "\tYour name, please? (3 to 15 characters)\n"
	import re
	myname = raw_input('Name? >')
	if len(myname) > 15 or len(myname) < 3:
		print "\nError! 3 to 15 characters, please!\nWe'd like to identify you properly."
		introduction()
	else:
		print "\n\t Welcome to Starbase Z, %r" % (myname)
		christen()
		
def christen():
	global myship
	print "\t\nYou have been assigned a medium-grade scout ship."
	print "\t\nPlease christen your ship (3 to 15 characters)."
	import re
	myship = raw_input('Ship Name? >')
	if len(myship) > 15 or len(myship) < 3:
		print "\nError! 3 to 15 characters, please!\nWe'd like to be able to identify your ship in case of \n ... accidents."
		christen()
	else:
		print "\nIt looks like you might survive with the %s at your command \n" % (myship)
		if justdied == True:
			spacedock()

def startingskills():
	print "The maximum a rating can reach in any one area is 100.\n"
	time.sleep(1)
	print "PILOTING affects your ability to dodge and hit in combat. \n"
	time.sleep(1)
	print "DIPLOMACY affects your ability to settle conflicts peacefully, \n acquire better deals on goods and services, and even influence other sentient beings. \n"
	time.sleep(1)
	print "SCIENG allows you to repair your ship in a more cost-effective way. \n It also affects your ability to use better spacecraft technology." 
	
def initialskills():
	global mypilot
	global myscieng
	global mydiplomacy
	print "\n\tWe have evaluated your attributes."
	time.sleep(1)
	
	mypilot = randint(10,25)
	mydiplomacy = randint(5,20)
	myscieng = randint(5,20)
	print """\nYou begin with the following:
	PILOTING ... %d
	DIPLOMACY .. %d
	SCIENG ..... %d
	""" % (mypilot, mydiplomacy, myscieng)
	time.sleep(1)
	print "Is acceptable -- Y or N?"
	choice = raw_input(' >')
	if choice == "Y" or choice == "y":
		print "\n\tLet's move on to your specialization process."
	else: 
		initialskills()
		
def checkfordiplomacy():
	global alienrace
	global alienvar
	print "Would you like to (F)ight or (N)egotiate with the enemy?"
	dipchoice = raw_input('F or N >')
	if dipchoice == "f" or dipchoice == "F":
		simulatebatt()
		combatroutine()
	elif dipchoice == "N" or dipchoice == "n":
		negotiateroutine()
	else:
		checkfordiplomacy()

def negotiateroutine():
	global mydiplomacy
	global mycredits
	global adddiplomacy
	global alienrace
	global alienvar
	global diplomacyroll
	global totalconflicts
	global myfame
	
	print "You attempt to negotiate a truce."
	diplomacyroll = randint(0,100)
	print diplomacyroll
	print mydiplomacy
	if diplomacyroll < mydiplomacy:
		print "Your attempt to broker a truce was successful.\nYou escape with your life."
		adddiplomacy = randint(1,6)
		mydiplomacy = mydiplomacy + adddiplomacy
		myfame = myfame + adddiplomacy
		checkskills()
		totalconflicts += 1
		print "Your diplomacy skill is now %d" % (mydiplomacy)
		print "Your fame has increased.  It is now %d." % (myfame)
		diplomchoice1 = raw_input("Would you like to continue voyaging, Y or N?>")
		if diplomchoice1 == "Y" or diplomchoice1 == "y":
			voyage()
		else: 
			spacedock()
	else:
		print "Your attempt fails.\n"
		print "You MUST FIGHT!"
		simulatebatt()
		combatroutine()					
		
def checkskills():
	global mypilot
	global myscieng
	global mydiplomacy
	global myhull
	global myhitchance
	global enemyhitchance
	global mywep
	
	
	if mypilot > 100:
		mypilot = 100
	else:
		mypilot = mypilot
	if myscieng > 100:
		myscieng = 100
	else:
		myscieng = myscieng
	if mydiplomacy > 100:
		mydiplomacy = 100
	else:
		mydiplomacy = mydiplomacy
	if myhull > 100:
		myhull = 100
	else:
		myhull = myhull
	if enemyhitchance < 0:
		enemyhitchance = 0
	elif enemyhitchance > 100:
		enemyhitchance = 100
	else: 
		enemyhitchance = enemyhitchance
	if myhitchance < 0:
		myhitchance = 0
	elif myhitchance > 100:
		myhitchance = 100
	else:
		myhitchance = myhitchance
	if mywep > 100:
		mywep = 100
	else: 
		mywep = mywep
		
def training():
	global mycredits
	if mycredits < 50:
		print "\t Training costs 50 credits per point of skill."
		print "\t You have insufficient funds for training at this time."
		spacedock()
	print """You may train in the follow areas:\n
	Diplomacy (D)
	Piloting (P)
	Science and Engineering (S)"""
	trainingchoice = raw_input(' >')
	if trainingchoice == "D" or trainingchoice == "d":
		trainindip()
	elif trainingchoice == "P" or trainingchoice == "p":
		traininpilot()
	elif trainingchoice == "S" or trainingchoice == "s":
		traininscience()
	else:
		training()

def traininscience():
	global myscieng
	global mycredits
	global pointstomaxsci
	pointspossible = mycredits / 50
	
	if pointspossible >= pointstomaxsci:
		print "The most skill you can buy is %d points." % (pointstomaxsci)
		print "How many points would you like to add to your SCIENG skill (1 to %d)?" % (pointstomaxsci)
		try:
			tpscieng = int(raw_input('> '))
		except ValueError:
			traininscience()
		else:
			if tpscieng > pointstomaxsci:
				print "You can only buy up to %d points of skill." % (pointstomaxsci)
				traininscience()
			elif tpscieng <= pointstomaxsci and tpscieng > 0:
				mycredits = mycredits - (tpscieng*50)
				myscieng = myscieng + tpscieng
				checkskills()
				print "\n\tYour training has yielded excellent results. \n\tYour new skill in SCIENG is now %d." % (myscieng)
				print "\nYou have %d credits remaining." % (mycredits)
			else:
				traininscience()
	elif pointspossible < pointstomaxsci and pointspossible >= 1:
		print "You can buy up to %d points of SCIENG skill" % (pointspossible)
		print "How many points would you like to add to your SCIENG skill (1 to %d)?" % (pointspossible)
		try:
			tpscieng = int(raw_input(' >'))
		except ValueError:
			traininscience()
		else:
			if tpscieng > pointspossible:
				print "You can only buy up to %d points of skill." % (pointspossible)
				traininscience()
			elif tpscieng <= pointspossible and tpscieng > 0:
				mycredits = mycredits - (tpscieng*50)
				myscieng = myscieng + tpscieng
				checkskills()
				print """Your training has yielded excellent results. 
				Your new skill in SCIENG is now %d.
				You have %d credits remaining.""" % (myscieng, mycredits)
				spacedock()
			else:
				traininscience()
	elif myscieng == 100:
		print "You are already at maximum level for this skill."
		print "Please return to the dock."
		spacedock()
	else: 
		spacedock()

		
def trainindip():
	global mydiplomacy
	global mycredits
	global pointstomaxdip
	
	pointspossible = mycredits / 50
	
	if pointspossible >= pointstomaxdip:
		print "You may train up to %d points." % (pointstomaxdip)
		print "How many points would you like to add to your DIPLOMACY skill (1 to %d)?" % (pointstomaxdip)
		try:
			tpdiplomacy = int(raw_input('> '))
		except ValueError:
			trainindip()
		else:
			if tpdiplomacy > pointstomaxdip:
				trainindip()
			elif tpdiplomacy <= pointstomaxdip and tpdiplomacy > 0:
				mycredits = mycredits - (tpdiplomacy*50)
				mydiplomacy = mydiplomacy + tpdiplomacy
				checkskills()
				print "\n\tYour training has yielded excellent results. \n\tYour new skill in DIPLOMACY is now %d." % (myscieng)
				print "\nYou have %d credits remaining." % (mycredits)
			else:
				trainindip()
	elif pointspossible < pointstomaxdip and pointspossible >= 1:
		print "You can buy up to %d points of DIPLOMACY skill" % (pointspossible)
		print "How many points would you like to add to your DIPLOMACY skill (1 to %d)?" % (pointspossible)
		try:
			tpdiplomacy = int(raw_input(' >'))
		except ValueError:
			trainindip()
		else:
			if tpdiplomacy > pointspossible:
				print "You can only buy up to %d points of skill." % (pointspossible)
				trainindip()
			elif tpdiplomacy <= pointspossible and tpdiplomacy > 0:
				mycredits = mycredits - (tpdiplomacy*50)
				mydiplomacy = mydiplomacy + tpdiplomacy
				checkskills()
				print """Your training has yielded excellent results. 
				Your new skill in DIPLOMACY is now %d.  
				You have %d credits remaining.""" % (mydiplomacy, mycredits)
				spacedock()
			else:
				trainindip()
	elif mydiplomacy == 100:
		print "You are already at maximum level for this skill."
		print "Please return to the dock."
		spacedock()
	else: 
		spacedock()
		
def traininpilot():
	global mypilot
	global mycredits
	global pointstomaxpilot
	pointspossible = mycredits / 50
	
	if pointspossible >= pointstomaxpilot:
		print "The most skill you can buy is %d points." % (pointstomaxpilot)
		print "How many points would you like to add to your PILOTING skill (1 to %d)?" % (pointstomaxpilot)
		try:
			tpscieng = int(raw_input('> '))
		except ValueError:
			traininpilot()
		else:
			if tppilot > pointstomaxpilot:
				print "You can only buy up to %d points of skill." % (pointstomaxpilot)
				traininscience()
			elif tpscieng <= pointstomaxpilot and tppilot > 0:
				mycredits = mycredits - (tppilot*50)
				myscieng = myscieng + tppilot
				checkskills()
				print "\n\tYour training has yielded excellent results. \n\tYour new skill in PILOTING is now %d." % (mypilot)
				print "\nYou have %d credits remaining." % (mycredits)
			else:
				traininpilot()
	elif pointspossible < pointstomaxpilot and pointspossible >= 1:
		print "You can buy up to %d points of PILOTING skill" % (pointspossible)
		print "How many points would you like to add to your PIOTING skill (1 to %d)?" % (pointspossible)
		try:
			tppilot = int(raw_input(' >'))
		except ValueError:
			traininpilot()
		else:
			if tppilot> pointspossible:
				print "You can only buy up to %d points of skill." % (pointspossible)
				traininpilot()
			elif tppilot <= pointspossible and tppilot > 0:
				mycredits = mycredits - (tppilot*50)
				mypilot = mypilot + tppilot
				checkskills()
				print """Your training has yielded excellent results. 
				Your new skill in PILOTING is now %d.
				You have %d credits remaining.""" % (mypilot, mycredits)
				spacedock()
			else:
				traininpilot()
	elif mypilot == 100:
		print "You are already at maximum level for this skill."
		print "Please return to the dock."
		spacedock()
	else: 
		spacedock()

def simulatebatt():
	global sim
	global sleepytime
	global battlespeed
	print "Simulate battle? Y or N?"
	simchoice = raw_input(' >')
	if simchoice == "N" or simchoice == "n":
		sim = False
	else:
		sim = True
		sleepytime = 0

def anykey():
	print "Hit any key to continue"
	choice2 = raw_input(' >')

#mainprogram
clearscreen()
saveorload()
startingskills()
initialskills()
specialization()
spacedock()
 	

