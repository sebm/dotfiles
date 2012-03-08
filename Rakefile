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

def restore_files(filenames, from_dir)
  # don't want to restore files if the working copy is dirty
  dirty_filecount = `git status --porcelain | wc -l`.to_i
  unless dirty_filecount == 0
    abort "ERROR: your dotfiles working copy is not clean."
  end

  filenames.each do |f|
    path_from = File.join(File.dirname(__FILE__), from_dir, f)
    path_to = File.expand_path(File.join('~', f))
    sh "cp #{path_from} #{path_to}"
  end

end

namespace :restore_dotfiles do
  desc "Restore zsh dotfiles to home directory"
  task :zsh do
    restore_files(zsh_dotfiles, 'zsh')
  end

  desc "Restore vim dotfiles to home directory"
  task :vim do
    restore_files(vim_dotfiles, 'vim')
  end

  desc "Restore all dotfiles to home directory"
  task :all => [:vim, :zsh] do
    puts "Restored all dotfiles to home directory"
  end
end

namespace :backup_dotfiles do
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
task :restore_dotfiles => "restore_dotfiles:all"


