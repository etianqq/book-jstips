# 中介者模式

几个对象之间不直接通话，而是通过一个中介者进行通信，从而促进形成宋耦合。

例子： [http://www.jspatterns.com/book/7/mediator.html](http://www.jspatterns.com/book/7/mediator.html)

    // player constructor
    function Player(name) {
        this.points = 0;
        this.name = name;
    }
    // play method
    Player.prototype.play = function () {
        this.points += 1;
        mediator.played();
    };

    // the scoreboard object
    var scoreboard = {

        // HTML element to be updated
        element: document.getElementById('results'),

        // update the score display
        update: function (score) {

            var i, msg = '';
            for (i in score) {
                if (score.hasOwnProperty(i)) {
                    msg += '<p><strong>' + i + '<\/strong>: ';
                    msg += score[i];
                    msg += '<\/p>';
                }
            }
            this.element.innerHTML = msg;
        }
    };


    var mediator = {

        // all the players
        players: {},

        //
        setup: function () {
            var players = this.players;
            players.home = new Player('Home');
            players.guest = new Player('Guest');

        },

        // someone plays, update the score
        played: function () {
            var players = this.players,
                    score = {
                        Home: players.home.points,
                        Guest: players.guest.points
                    };

            scoreboard.update(score);
        },

        // handle user interactions
        keypress: function (e) {
            e = e || window.event; // IE
            if (e.which === 49) { // key "1"
                mediator.players.home.play();
                return;
            }
            if (e.which === 48) { // key "0"
                mediator.players.guest.play();
                return;
            }
        }
    };


    // go!
    mediator.setup();
    window.onkeypress = mediator.keypress;

    // game over in 30 seconds
    setTimeout(function () {
        window.onkeypress = null;
        alert('Game over!');
    }, 30000);
