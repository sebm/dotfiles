zsh_dotfiles = [
  '.zshenv',
  '.zshrc'
]

vim_dotfiles = [
  '.vimrc.after',
  '.vimrc.before',
  '.gvimrc.after'
]

def backup_files(filenames, dest)
  filenames.each do |f|
    path_to_dotfile = File.expand_path(File.join('~', f))

    if File.file? path_to_dotfile
      cp path_to_dotfile, File.join(File.dirname(__FILE__), dest, f)
    end
  end
end

namespace :backup_dotfiles do
  task :default => :all

  desc "Backup vim dotfiles to repostory"
  task :vim do
    backup_files(vim_dotfiles, 'vim')
  end

  desc "Backup zsh dotfiles to repository"
  task :zsh do
    backup_files(zsh_dotfiles, 'zsh')
  end

  desc "Backup all dotfiles to repository"
  task :all => [:vim, :zsh] do
    puts "Copied all dotfiles to repository"
  end
end

task :backup_dotfiles => "backup_dotfiles:all"

