class HerokuSassAndCacheController < ActionController::Base
  
  def stylesheets
    load_file_if_available('stylesheets', params[:file])
  end
  
  def javascripts
    load_file_if_available('javascripts', params[:file])
  end
  
  private
  
  def load_file_if_available(folder, file)
    tmp_file = File.join(Rails.root, 'tmp', folder, file)
    public_file = File.join(Rails.public_path, folder, file)
    
    if FileTest.exists?(tmp_file)
      if stale?(:etag => tmp_file, :last_modified => File.mtime(tmp_file).utc)
        render :file => tmp_file, :layout => false
      end
    elsif FileTest.exists?(public_file)
      if stale?(:etag => public_file, :last_modified => File.mtime(public_file).utc)
        render :file => public_file, :layout => false
      end
    else
      render :nothing => true, :status => 404
    end
  end
  
end