package com.unitseven.springboot;

import static org.junit.jupiter.api.Assertions.assertNull;
import static org.junit.jupiter.api.Assertions.assertFalse;

import static org.mockito.ArgumentMatchers.any;
import static org.mockito.Mockito.*;

import com.unitseven.springboot.Service.UsersService;
import com.unitseven.springboot.Entity.user;
import com.unitseven.springboot.repository.UserRepository;

import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.MockitoAnnotations;
import org.springframework.boot.test.context.SpringBootTest;

import java.util.Arrays;
import java.util.Optional;
import java.util.List;

import static org.junit.jupiter.api.Assertions.assertEquals;
import static org.junit.jupiter.api.Assertions.assertTrue;

@SpringBootTest
public class UserServiceTest {

    @Mock
    private UserRepository userRepository;

    @InjectMocks
    private UsersService userService;

    @BeforeEach
    public void setup() {
        MockitoAnnotations.openMocks(this);
    }
    
    @Test
public void whenSaveUser_thenReturnsUser() {
    user user = new user();
    user.setUser_id(1);
    user.setUsername("Test User");
    
    when(userRepository.save(any(user.class))).thenReturn(user);
    
    user savedUser = userService.saveUser(user);
    
    assertEquals(user.getUsername(), savedUser.getUsername());
    verify(userRepository).save(user);
}
    @Test
public void whenValidUserId_thenUserShouldBeFound() {
    Integer userId = 1;
    Optional<user> expectedUser = Optional.of(new user());
    
    
    when(userRepository.findById(userId)).thenReturn(expectedUser);
    
    Optional<user> foundUser = userService.getUserById(userId);
    
    assertTrue(foundUser.isPresent());
    assertEquals(expectedUser, foundUser);
}
    @Test
public void whenGetAllUsers_thenReturnsListOfUsers() {
    List<user> userList = Arrays.asList(new user(), new user());
    
    
    when(userRepository.findAll()).thenReturn(userList);
    
    List<user> retrievedUsers = userService.getAllUsers();
    
    assertEquals(2, retrievedUsers.size());
}
    @Test
public void whenDeleteUser_thenVerifyMethodCalled() {
    Integer userId = 1;
    
    userService.deleteUser(userId);
    
    verify(userRepository).deleteById(userId);
}

    @Test
public void whenSaveUserWithNullUser_thenReturnsNull() {
    user result = userService.saveUser(null);
    assertNull(result);
}
    @Test
public void whenGetUserByNonExistentId_thenEmptyResult() {
    Integer userId = Integer.MAX_VALUE; 
    when(userRepository.findById(userId)).thenReturn(Optional.empty());
    
    Optional<user> result = userService.getUserById(userId);
    
    assertFalse(result.isPresent());
}
    @Test
public void whenGetUserByExtremeId_thenEmptyResult() {
    Integer userId = -1; 
    when(userRepository.findById(userId)).thenReturn(Optional.empty());
    
    Optional<user> result = userService.getUserById(userId);
    
    assertFalse(result.isPresent());
}


}
