# Gitlab Package for Arch Linux

# Configuration

    pacman -S gitlab
    Edit /home/git/gitlab/config/config.yml
    Edit /home/git/gitlab/config/database.yml (default is postgres, use database.yml.mysql for mysql)

# Check

    cd /home/git/gitlab
    bundle exec rake gitlab:check RAILS_ENV=production

# Run

    systemctl start gitlab