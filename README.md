horriblepeople
==============

DB SCHEMA
==============
SESSIONS:
	pk_session
	user_pk
	date_started
	date_last_active
	fb_token
	date_fb_token_expires
USERS:
	pk_user
	username
	fbid
	date_first_registered
	is_active
	num_games_won
	num_games_lost
	num_games_started
	num_cards_accepted
	num_rounds_won
GAMES:
	pk_game
	user_pk_creator
	user_pk_owner
	date_started
	date_ended
	name
	cur_round
	max_rounds
	max_wait_time
GAME_MEMBERS:
	pk_game_member
	round_joined
	rounds_won
	user_pk
	game_pk
GAME_TOPICS:
	pk_game_topic
	game_pk
	date_submitted
	round_no
	user_pk_judge
	card_pk_topic
GAME_SUBMISSIONS:
	pk_game_submission
	date_submitted
	(game_pk)
	game_topic_pk
	user_pk_submitor
	card_pk_submission
CARDS:
	pk_card
	card_type: {topic, submission}
	is_active
	text
	date_suggested
	date_last_activation_state_change
	upvotes
	downvotes
NOTIFICATIONS:
	?

SERVER API
==============
GET /login/facebook				starts a session, register user if necessary (though fb auth)
GET /logout						ends the session
GET /unregister					user removed the app

(POST /users/block				block a user)

GET /games/list					list the games the user is in (including ended games)
POST /games/new					create a new game
POST /games/edit				edit a game metadata
POST /games/mebership/add		add a player to a game
POST /games/membership/remove	kick a player out of a game
POST /games/leave				leavea a game
(POST /games/block				block requests from a game)
(POST /games/transfer			transfer ownership of a game)

POST /games/play/start			start a game
POST /games/play/topic			select the topic for the newt round of the game
POST /games/play/submission		submit a card for the round
GET /games/play/review			review the submissions for the last round
POST /games/play/select			select a winner of the round
GET /games/history				view the history of a game

GET /cards/suggestions/review	review an un-accepted card and rate it
POST /cards/suggestions/rate	submit a rating for an un-accepted card

GET /notifications/list			?
?


QUESTIONS
=============
1. how to store/display/push notifications?
2. how to make sure cards don't get repeated in a game?
3. how to make sure the number of accepted cards stays at some minimum level?