# PRしたファイルの直近のコミット履歴を表で可視化する

files = (git.added_files + git.modified_files) #=> FileList

markdown "## あなたが修正したファイルに関する直近のコミット\n\n"
data = []
reviewer = nil
files.each do |f|
	# gitからそのファイルの履歴を取得する
	#logs = git.git.gblob(f).log(5)
	logs = git.commits

	message = "### #{f}\n\n"
	message << "date | commit | msg | user |\n"
	message << "| --- | ----- | --- | --- |\n"

	tmp = []
	logs.each do |log|
		d = {
			:user => log.author.name,
			:id => log,
			:date => log.date,
			:msg => log.message,
		}
		tmp.push(d)
	    message << "| #{d[:date]} | #{d[:id]} | #{d[:msg]} | #{d[:user]} |\n"	

		# TODO ??
		reviewer = d[:user]
	end

	data.push(tmp)
	message << "\n\n"
	markdown message

	# TODO 直近のコミッタをレビューアに設定する
	
end

github.pr_json["reviewers"] = reviewer
message "#{reviewer}さんをレビューアにします"

