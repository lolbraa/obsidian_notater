# GitHub
## create a new repository on the command line
```
echo "# gitops_lolbraa_tailscale" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:lolbraa/gitops_lolbraa_tailscale.git
git push -u origin main
```

## push an existing repository from the command line
```
git remote add origin git@github.com:lolbraa/gitops_lolbraa_tailscale.git
git branch -M main
git push -u origin main
```

# git.ncgas.no

## Bruke keyring til å lagre access tokens trygt
[Authentication - Git Documentation - Obsidian Publish](https://publish.obsidian.md/git-doc/Authentication#Storing)
```sh
sudo apt install libsecret-1-0 libsecret-1-dev make gcc

sudo make --directory=/usr/share/doc/git/contrib/credential/libsecret

# NOTE: This changes your global config, in case you don't want that you can omit the `--global` and execute it in your existing git repository.
git config --global credential.helper \
   /usr/share/doc/git/contrib/credential/libsecret/git-credential-libsecret
```
## Lagre i klartekst
```
git config --global credential.helper "cache --timeout=86400"
```
eller for evig lagring:
```
git config --global credential.helper store
```