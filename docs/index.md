# Team Waterloop

Canada's Hyperloop, designed and built at the University of Waterloo.
This is the documentation hub for all components of our pod.

This site is not intended for sharing outside of the team.

## How to contribute

- `git clone https://github.com/teamwaterloop/docs`
- Edit the relevant files in the `docs` folder.
- `git commit -m "<a brief descriptive message about what you added>"`
- `git push origin master`

After pushing, the updated documentation will be compiled and deployed to 
[docs.teamwaterloop.ca](https://docs.teamwaterloop.ca) within a couple of minutes.

## Building locally

To build locally, you need to first install Python, then do the following:

- `pip install mkdocs mkdocs-cinder`
- `mkdocs build`
- `cd site`
- If Python 3: `python -m http.server 4000`
- If Python 2: `python -m SimpleHTTPServer 4000`
- And then navigate to `localhost:4000` to see your work!
