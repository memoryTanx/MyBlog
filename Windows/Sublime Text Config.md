### Sublime Text Settings

```js
// D:\IDE\Sublime Text\Data\Packages\User\Preferences.sublime-settings

{
	"color_scheme": "Mariana.sublime-color-scheme",
	"translate_tabs_to_spaces": true,

	"save_on_focus_lost": true,

	// "font_face": "Consolas-with-Yahei",
	/*"font_size": 11,*/
	"show_encoding": true,
	// "font_options": ["gdi"],
	// "dpi_scale": 1.0,

	"word_wrap": false,

	"rulers": [72, 119],

	"default_line_ending": "unix",
	
	"show_definitions": false,

	"show_line_endings": true,

	"index_exclude_gitignore": false,
	"font_size": 12,

	"read_only_mode": true,
	"theme": "auto",
}

```

### readonly 插件
```python
# D:\IDE\Sublime Text\Data\Packages\readonly\readonly.py

import sublime
import sublime_plugin


class ToggleReadonlyModeCommand(sublime_plugin.TextCommand):
    def run(self, edit):
        if (self.view.is_read_only()):
            self.view.set_read_only(False)
            self.view.set_status('read_only_mode', 'writeable')
            self.view.window().status_message("View " + str(self.view.file_name()) + " is writeable.")
        else:
            self.view.set_read_only(True)
            self.view.set_status('read_only_mode', 'readonly')
            self.view.window().status_message("View " + str(self.view.file_name()) + " is readonly.")


class ToggleReadonlyListener(sublime_plugin.EventListener):
    def on_load(self, view):
        """仅对venv文件夹的文件【只读】"""

        if 'venv' in view.file_name():

            if view.settings().get('read_only_mode'):
                view.set_read_only(True)
                view.set_status('read_only_mode', 'readonly')
                view.window().status_message("View " + str(view.file_name()) + " is readonly.")


```

&

```js
// D:\IDE\Sublime Text\Data\Packages\readonly\Context.sublime-menu

[
    {
        "caption": "Toggle Readonly mode",
        "command": "toggle_readonly_mode",
        
    }
]

```

https://packagecontrol.io/
