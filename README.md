# 35_36e_front

just text

**bold text**

--italic text--

```java

package org.anefdev.bookeeper.service;

import lombok.RequiredArgsConstructor;
import org.anefdev.bookeeper.dto.BookDTO;
import org.anefdev.bookeeper.dto.BookDtoConverter;
import org.anefdev.bookeeper.exception.BookAlreadyExistsException;
import org.anefdev.bookeeper.repository.BookRepository;
import org.springframework.stereotype.Service;

import java.util.List;

@Service
@RequiredArgsConstructor
public class BookService {


    private final BookRepository repository;

    public List<BookDTO> getAll() {

        return BookDtoConverter.convertListOfBooksToDTO(repository.findAll());

    }

    public void saveBook(BookDTO bookDto) throws BookAlreadyExistsException {

        if (repository.findBooksByTitleContaining(bookDto.getTitle()).isEmpty()) {

            repository.save(BookDtoConverter.convertBookDTOtoBookEntity(bookDto));

        } else {
            throw new BookAlreadyExistsException("BOOK WITH TITLE: " + bookDto.getTitle() + " ALREADY EXISTS");
        }
    }

    public List<BookDTO> findBooksByTitle(String title) {

        return BookDtoConverter.convertListOfBooksToDTO(repository.findBooksByTitleContaining(title));

    }

    public List<BookDTO> findBooksByAuthor(String author) {

        return BookDtoConverter.convertListOfBooksToDTO(repository.findBooksByAuthorContaining(author));

    }

}
```
