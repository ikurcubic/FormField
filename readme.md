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

Begin by installing the package through Composer.

    require: {
        "way/form": "dev-master"
    }

Next, add the service provider to `app/config/app.php`.

    'providers' => [
        // ..
        'Way\Form\FormServiceProvider'
    ]

That's it! You're all set to go. Try it out in a view:

    {{ FormField::username() }}
    {{ FormField::email() }}
    {{ FormField::custom(['type' => 'textarea']) }}
    {{ FormField::address(['label' => 'Your Address']) }}

If you want to override the defaults, you can, publish the config, like
so:

    php artisan config:publish way/form
