This is just a Laravel forms idea, whipped together in a half-hour. Play around with
it, if you wish. If people enjoy it, I'll clean it up, make it more
flexible, and turn it into a package.

The basic idea is simple: make form creation simpler. I'm tired of
creating form fields, like this:

    <div class="form-group">
        {{  Form::label('username', 'Username:' ) }}
        {{ Form::text('username', null, ['class' => 'control-group']) }}
    </div>

Instead, with this `FormField` class, you can simply do:

    {{ FormField::username() }}

That will then produce the necessary HTML. It uses dynamic methods to
simplify the process a bit.

While it will do its best to figure out what kind of input you want, you
can override it.

    {{ FormField::yourBio(['type' => 'textarea']) }}

This will produce:

    <div class='form-group'>
        <label for="yourBio">Your Bio: </label>
        <textarea class="form-control" type="textarea" name="yourBio" cols="50" rows="10" id="yourBio"></textarea>
    </div>

Okay, that's it. Like I said, just an idea. Good, bad, lame?

## Usage

To try this out:

1. Download the `FormField` class
2. Add it anywhere you want. Maybe `app/FormField.php`.
3. Autoload that class from your `composer.json` file:

It might look like this:

	"autoload": {
		"classmap": [
			// ...
			"app/FormField.php"
		]
	}

Finally, `composer dump-autoload`, and the class is ready to toy with.
Try it out in a view:

    {{ FormField::username() }}
    {{ FormField::email() }}
    {{ FormField::custom(['type' => 'textarea']) }}
    {{ FormField::address(['label' => 'Your Address']) }}

If you want to override the defaults, you can, somewhere in your app,
call:

    FormField::setDefaults([
        'wrapper' => 'li',
        'wrapperClass' => 'my-form-field',
        'inputClass' => 'class-to-be-put-on-input'
    ]);
