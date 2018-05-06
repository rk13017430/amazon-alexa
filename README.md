# amazon-alexa
skill to improve functioning of amazon alexa
from __future__ import print_function



def build_speechlet_response(output, should_end_session):
    return {
        'outputSpeech': {
            'type': 'PlainText',
            'text': output
        },
        'shouldEndSession': should_end_session
    }


def build_response(speechlet_response):
    return {
        'version': '1.0',
        'response': speechlet_response
    }


# --------------- Functions that control the skill's behavior ------------------

def get_quote():
    import random
    x = random.randint(0,42)
    print(x)
    quotes = ['Friendship is always a sweet responsibility, never an opportunity', 'True friendship is when you walk into their house and your WiFi connects automatically.', 'True friendship multiplies the good in life and divides its evils. Strive to have friends, for life without friends is like life on a desert island to find one real friend in a lifetime is good fortune to keep him is a blessing.', 'The language of friendship is not words but meanings', 'Friendship is the only cement that will ever hold the world together.', 'Do not walk behind me I may not lead. Do not walk in front of me I may not follow. Just walk beside me and be my friend. ', 'True friendship comes when the silence between two people is comfortable.', 'Friendship is born at that moment when one person says to another What You too I thought I was the only one.', 'Friendship consists in forgetting what one gives and remembering what one receives.', 'Be slow to fall into friendship but when thou art in, continue firm & constant.', 'Friendship is like money, easier made than kept', 'A friend is one that knows you as you are, understands where you have been, accepts what you have become, and still, gently allows you to grow.', 'Anybody can sympathize with the sufferings of a friend, but it requires a very fine nature to sympathise with a friends success. ', 'I do not need a friend who changes when I change and who nods when I nod my shadow does that much better. ', 'Wishing to be friends is quick work, but friendship is a slow ripening fruit.', 'A good friend can tell you what is the matter with you in a minute. He may not seem such a good friend after telling. ', 'There is nothing better than a friend, unless it is a friend with chocolate.', 'Lots of people want to ride with you in the limo, but what you want is someone who will take the bus with you when the limo breaks down. ', 'A friend is someone who knows all about you and still loves you', 'Do I not destroy my enemies when I make them my friends', 'Let us be grateful to people who make us happy, they are the charming gardeners who make our souls blossom', 'An insincere and evil friend is more to be feared than a wild beast a wild beast may wound your body, but an evil friend will wound your mind.', 'Its the friends you can call up at 4 a.m. that matter.', 'My best friend is the one who brings out the best in me.', 'Friendship is the hardest thing in the world to explain. Its not something you learn in school. But if you have not learned the meaning of friendship, you really have not learned anything. ', 'Sometimes being a friend means mastering the art of timing. There is a time for silence. A time to let go and allow people to hurl themselves into their own destiny. And a time to prepare to pick up the pieces when it is all over. ', 'There is a magnet in your heart that will attract true friends. That magnet is unselfishness, thinking of others first when you learn to live for others, they will live for you.', 'Love is blind friendship closes its eyes.', 'Friendship is unnecessary, like philosophy, like art It has no survival value; rather it is one of those things which give value to survival.', 'I think if I have learned anything about friendship, it is to hang in, stay connected, fight for them, and let them fight for you. Dont walk away, do not be distracted, do not be too busy or tired, dont take them for granted. Friends are part of the glue that holds life and faith together. ', 'The friend who holds your hand and says the wrong thing is made of dearer stuff than the one who stays away.', 'I value the friend who for me finds time on his calendar, but I cherish the friend who for me does not consult his calendar.', 'Sweet is the memory of distant friends! Like the mellow rays of the departing sun, it falls tenderly, yet sadly, on the heart. ', 'How many slams in an old screen door? Depends how loud you shut it. How many slices in a bread? Depends how thin you cut it. How much good inside a day? Depends how good you live em. How much love inside a friend? Depends how much you give em.', 'Growing apart doesnt change the fact that for a long time we grew side by side; our roots will always be tangled. I am glad for that.', 'Friends are the family you choose', 'We cannot tell the precise moment when friendship is formed. As in filling a vessel drop by drop, there is at last a drop which makes it run over; so in a series of kindnesses there is at last one which makes the heart run over.', 'Never leave a friend behind. Friends are all we have to get us through this life and they are the only things from this world that we could hope to see in the next.', 'Tis the privilege of friendship to talk nonsense, and to have her nonsense respected.', 'The glory of friendship is not the outstretched hand, not the kindly smile, nor the joy of companionship; it is the spiritual inspiration that comes to one when you discover that someone else believes in you and is willing to trust you with a friendship.', 'A friendship that can end never really began', 'No person is your friend who demands your silence, or denies your right to grow', 'In prosperity our friends know us; in adversity we know our friends.', 'You can always tell a real friend: when youve made a fool of yourself he doesnt feel youve done a permanent job. ', 'You can make more friends in two months by becoming interested in other people than you can in two years by trying to get other people interested in you', 'Some people go to priests, others to poetry, I to my friends. ', 'The real test of friendship is can you literally do nothing with the other person? Can you enjoy those moments of life that are utterly simple?', 'Friendship improves happiness, and abates misery, by doubling our joys, and dividing our grief.', 'Do not save your loving speeches']
    speech_output = quotes[x]

    should_end_session = True
    return build_response(build_speechlet_response(
        speech_output, should_end_session))





# --------------- Events ------------------

def on_session_started(session_started_request, session):
    """ Called when the session starts """

    print("on_session_started requestId=" + session_started_request['requestId']
          + ", sessionId=" + session['sessionId'])


def on_launch(launch_request, session):

    print("on_launch requestId=" + launch_request['requestId'] +
          ", sessionId=" + session['sessionId'])
    # Dispatch to your skill's launch
    return get_quote()


def on_intent(intent_request, session):

    print("on_intent requestId=" + intent_request['requestId'] +
          ", sessionId=" + session['sessionId'])

    intent = intent_request['intent']
    intent_name = intent_request['intent']['name']

    return get_quote()



# --------------- Main handler ------------------

def lambda_handler(event, context):
    """ Route the incoming request based on type (LaunchRequest, IntentRequest,
    etc.) The JSON body of the request is provided in the event parameter.
    """
    print("event.session.application.applicationId=" +
          event['session']['application']['applicationId'])

    """
    Uncomment this if statement and populate with your skill's application ID to
    prevent someone else from configuring a skill that sends requests to this
    function.
    """
    # if (event['session']['application']['applicationId'] !=
    #         "amzn1.echo-sdk-ams.app.[unique-value-here]"):
    #     raise ValueError("Invalid Application ID")

    if event['session']['new']:
        on_session_started({'requestId': event['request']['requestId']},
                           event['session'])

    if event['request']['type'] == "LaunchRequest":
        return on_launch(event['request'], event['session'])
    elif event['request']['type'] == "IntentRequest":
        return on_intent(event['request'], event['session'])
    elif event['request']['type'] == "SessionEndedRequest":
        return on_session_ended(event['request'], event['session'])
