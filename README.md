# Live Project

## Django Project Introduction
  During the past two weeks I have been developing a hobby manager web application with my fellow peers in the Tech Academy. This application required a combination of computer languages in order to produce the full product. These languages include HTML, CSS, 
Python, and Django. Throughout this project I have learned the important factors that go into creating a website based off of multiple templates and the inheritance between them. In order to get each part of the application to work together, a combination of both Python and Django were used on the back end so that each file was linked properly. These links include button functions, url mapping, and the ability to communicate with a database. The usage of the database was important for saving useful data related to the given hobby application.

  With multiple languages working together, bugs and errors were bound to occur. Thankfully, I was able to overcome those unforseen obstacles and turn them into learning opportunities which in hand is very valuable. Iam proud of what I have created, and Iam fortunate for the opportunity to work with other peers and collaborate all I have been learning. 

## HTML Templates
  One of the biggest factors for this project was the usage of webpage templates and connecting each page together through inhertiance. This was able to be completed by first creating a base parent template that each page created after would have to follow. My application was focused on creating a list of football games and details about that game. My base template revolved around creating a game, and viewing past games created by the user. Here is an example of what the code looks like behind viewing past games. 
  
        <table class="table">
            <tr>
                <th class="col-md">Opponent:</th>
                <th class="col-md">Stadium:</th>
                <th class="col-md">Time of Day:</th>
                <th class="col-md">Significance:</th>
                <th class="col-md">Score:</th>
                <th class="col-md">Winner:</th>
            </tr>
            {% for game in games %}
                <tr>
                    <td class="col-md">{{game.against}}</td>
                    <td class="col-md">{{game.stadium}}</td>
                    <td class="col-md">{{game.time_of_day}}</td>
                    <td class="col-md">{{game.significance}}</td>
                    <td class="col-md">{{game.score}}</td>
                    <td class="col-md">{{game.win_loss}}</td>
                </tr>
            {% endfor %}
        </table>
        
## Database Model
  Another important factor of this project was that usage of a database. Setting up user inputs was a must as there needed to be some way to communicate to the database with the user. This was mainly done through the use of Django and built in models to create a database. This page is one of the bigger pages in terms of functionality because it is what recorded the inputs and sent them to a given table. Based off of the primary keys in this table, a more in depth details page was able to be created. By calling the primary key, a link was able to be created that would identify any specific row in the table. This is an example of what the model looked like for recording user input.
  
  Team_Against = (('South Florida', 'South Florida'), ('Louisiana State University', 'Louisiana State University'),
                ('Kansas State', 'Kansas State'), ('Oklahoma State', 'Oklahoma State'), ('Oklahoma', 'Oklahoma'),
                ('West Virginia', 'West Virginia'), ('Texas Tech', 'Texas Tech'), ('Baylor', 'Baylor'),
                ('Kansas', 'Kansas'), ('Iowa State', 'Iowa State'),
                ('Texas Christian University', 'Texas Christian University'), ('Other', 'Other'))

  Home_Away = (('Home', 'Home'), ('Away', 'Away'), ('Other', 'Other'))
  Game_Time = (('Morning', 'Morning'), ('Afternoon', 'Afternoon'), ('Evening', 'Evening'), ('Other', 'Other'))
  Game_Importance = (('0', '0'), ('1', '1'), ('2', '2'), ('3', '3'), ('4', '4'), ('5', '5'),
                   ('6', '6'), ('7', '7'), ('8', '8'), ('9', '9'), ('10', '10'))
  Win_Loss = (('Texas', 'Texas'), ('Opponent', 'Opponent'))


  class TexasGame(models.Model):
      win_loss = models.CharField(max_length=20, choices=Win_Loss)
      stadium = models.CharField(max_length=20, choices=Home_Away)
      against = models.CharField(max_length=75, choices=Team_Against)
      time_of_day = models.CharField(max_length=20, choices=Game_Time)
      score = models.PositiveIntegerField(blank=True, null=True)
      significance = models.CharField(max_length=20, choices=Game_Importance)
      
## Functions
  In order for the application to work, a must is back end functions that are doing the work which they are being called on for. Some of this work included creating the form for user input, a function to show a list of the recorded inputs, and a function for accessing specific entries through their primary key from the database. A request would be sent to any of the given functions that are called upon, and based off of the called function a certain result would be returned and rendered. This was done through the use of a url file. This file was basically the middle-man between the front end and the back end functions. Here is an example of what the functions looked like for viewing all entries, and for creating new ones. 
  
  def index(request):
    get_games = TexasGame.TexasGames.all()
    context = {'games': get_games}
    return render(request, 'TexasScore/TexasScore_index.html', context)


  def create_game(request):
      form = TexasForm(request.POST or None)
      if form.is_valid():
          form.save()
          return redirect('giveGames')
      else:
          print(form.errors)
          form = TexasForm()
      return render(request, 'TexasScore/TexasScore_create.html', {'form': form})

The function labeled index was responsible for viewing all entries in a given format. This format is applied after the function returns the request back to the caller. The format is labled on the index html page. The create_game function was responsible for creating the form for user input then saving it. After the entry is saved, the user is returned to the orginal page seen for creating the entry in the first place. This way multiple entries could be made without the user having to self direct back to form page. 

## Outro
  After two weeks of working with peers, and simulating a real-life workplace, I have learned more than I had imagined. I learned from every bug, obstacle, and completion. There is always more to learn about computer software but that is the nature of this area of development. Learning more in depth about how a certain language works, and why it works will continue to drive me on to learn more. I really enjoyed seeing my final product and intertwining different languages to produce an application. 
