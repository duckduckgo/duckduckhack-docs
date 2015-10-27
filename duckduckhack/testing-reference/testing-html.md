## Testing HTML

You should have already tested your triggers by following the [Testing triggers](https://duck.co/duckduckhack/testing_triggers) section. Now that you're confident your triggers are functioning properly, follow these steps to see how it looks on a live server!

<!-- /summary -->

1. Enter the root directory of your forked Instant Answer repository:

	Log in to Codio and visit the dashboard. In the menu, click Codio > [Dashboard](https://codio.com/home/projects)
	
	Click on the **DuckDuckHack project**, which you previously forked and cloned.
	
	Next, open a terminal window if it's not already open. (Tools > Terminal).
	
	At the command prompt, change into your repository directory, for example:
	
	```shell
	cd zeroclickinfo-goodies
	```

	The command line prompt will now indicate the repository and branch you are in, for example:
	
	```shell
	[ codio@border-carlo workspace zeroclickinfo-goodies {master}]$
	```

2. Type **`duckpan server`** and press "**Enter**". The Terminal should print some text and let you know that the server is listening on port 5000.

    ```shell
    Starting up webserver...

    You can stop the webserver with Ctrl-C

    HTTP::Server::PSGI: Accepting connections at http://0:5000/
    ```

3. Click the "**DuckPAN Server**" button at the top of the screen. A new browser tab should open and you should see the DuckDuckGo Homepage.	
	
    You should now be able to search and see live Instant Answer results. The server runs code from our site which should make it look very much like the real DuckDuckGo.

4. Search.

    Having already tested your triggers, you should be able to construct a query to hit that trigger and see your newly defined result. Information about the processing of your requests is printed to the terminal where you started the server. Any external API calls will be highlighted if supported by your terminal.

5. Debug.

    If your search doesn't hit an Instant Answer, there will be an error message displayed on the page: "Sorry, no hit for your Instant Answer."

  If the trigger is hit but you do not see something displayed on the screen, a number of things could be wrong:

    - You have a JavaScript error of some kind. Internally, we like to use the JavaScript console in [Firebug](http://getfirebug.com/) to get more details.

    - An external API was not called correctly. You should examine the Web server output to make sure the correct API is being called. If it's not you will need to revise your [Spice handle function](https://duck.co/duckduckhack/spice_basic_tutorial#define-the-handle-function).

    - An external API did not return anything. Firebug is a great help here, as well. You should be able to see the external call in your browser and examine the response.

6. Tweak the display.

    Once all of the processing is working properly, you will probably want to adjust your callback function to get the display just right. The [Display reference](https://duck.co/duckduckhack/display_reference) section has some pointers to help you along.

7. Document.

    Please document your code as appropriate using in-line comments.
