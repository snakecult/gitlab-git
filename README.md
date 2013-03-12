# Gitlab Package for Arch Linux

# Configuration

    pacman -S gitlab
    Edit /home/git/gitlab/config/config.yml
    Edit /home/git/gitlab/config/database.yml (default is postgres, use database.yml.mysql for mysql)

# Initialize Database

    sudo -u git -H bundle exec rake db:setup RAILS_ENV=production
    sudo -u git -H bundle exec rake db:seed_fu RAILS_ENV=production
    sudo -u git -H bundle exec rake gitlab:setup RAILS_ENV=production

# Check

    systemctl start sidekiq
    cd /home/git/gitlab
    bundle exec rake gitlab:check RAILS_ENV=production

# Run

    systemctl start gitlab